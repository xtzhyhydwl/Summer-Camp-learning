>开发板：STM32F103C8T6最小系统板，点亮LED呈现呼吸灯效果（本来想搞180度SG90舵机的结果手上没有）
# 1. 系统基本内核设置

- 设置为串口调试，外部时钟，时钟树如下，频率拉满到72MHz
![[Pasted image 20230801160317.png]]
![[Pasted image 20230801174157.png]]![[Pasted image 20230801162128.png]]

# 2. 定时器初始化

- 欲实现呼吸灯，并且清晰体现定时器PWM模式的功能，这里选用TIM2作为PWM generator，TIM3作为PWM占空比变化的时间度量（可以通过同时使能TIM2中断来计时，不推荐用，因为当时我没想起来:P）

- 配置TIM2通道1为PWM模式，PA0口会自动变为输出PWM的模式，注意通道与IO口的联系

![[Pasted image 20230801175521.png]]
其中一次重装是72M/72=1us，计数20k次为一个周期，所以PWM周期为50Hz
![[Pasted image 20230801175628.png]]

- 设置TIM3也为这个溢出频率，频率再高了也没用，因为在一个周期内改变多次CCR的值，溢出时的标准还是最后一个，中间的都被浪费了
![[Pasted image 20230801180102.png]]
记得开启TIM3的中断使能
![[Pasted image 20230801180131.png]]

# 3. keil代码

- 生成代码，全部编译。代码默认是全部功能关闭的，我们需要将TIM2的PWM打开，TIM3的IT打开，再写个TIM3的中断回调函数，实现PWM占空比随着时间增减，才算大功告成。

- 打开main.c，找到MX_TIM2_Init函数，看definition，再找到下方HAL_TIM_PWM_Init，看definition
![[Pasted image 20230801180556.png]]
![[Pasted image 20230801180632.png]]

- 从跳转到的地方查找PWM，直到看到关键词“start”，就是我们要找到函数（或者干脆搜PWM_Start，人生会更幸福）
![[Pasted image 20230801181044.png]]

- 把它丢到MX_TIM2_Init下面，两个参数分别是&htimx，TIM_CHANNEL_x，填上我们选的定时器通道即可
![[Pasted image 20230801181222.png]]

- PWM开启是重头戏，至于TIM3的中断开启的函数就在下方，不再赘述，接下来写一个简单的中断回调函数
![[Pasted image 20230801181642.png]]
![[Pasted image 20230801181424.png]]

- 有几点可讲，首先是使用自定义变量flag_reverse作为标志位，判断占空比是该增还是减；其次是使用了函数__HAL_TIM_SetCompare来直接设置compare值（计算时使用自定义中间变量Compare），这个函数的参数就多了个整数，表示设定的Compare值。

- TIM3中断溢出->改变Compare->改变占空比->LED灯亮度随时间变化->呼吸灯

# 4. 总结

- 成功学会TIM输出PWM，并且能手动改变占空比

- 如果只用TIM2,，也能实现呼吸灯，占用更少资源

- 乐:D