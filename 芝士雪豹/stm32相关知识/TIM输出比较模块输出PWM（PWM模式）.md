- 参考视频：【STM32入门教程-2023持续更新中】 https://www.bilibili.com/video/BV1th411z7sn/?p=15&share_source=copy_web&vd_source=1ca96e0b8c00193760c615cfbd038092

- （参考手册->13.3.10 PWM模式）

# 1. PWM概念

- PWM——脉冲宽度调制，在有惯性的系统中，用脉冲等效模拟信号

- PWM参数：
![[Pasted image 20230801154509.png]]
分辨率理解为等效的精度
# 2. TIM输出比较模式输出PWM原理

- 通用定时器中关于捕获比较模式的框图
![[Pasted image 20230801154911.png]]
![[Pasted image 20230801155044.png]]

- 对于两寄存器CNT和CCR，设置好数值之后，CNT自动计数。在特定模式下（TIMx_CCMRx寄存器控制），满足CNT和CCR之间某种大小关系，则会执行某种功能，下面是对照图
![[Pasted image 20230801155221.png]]

tips：有效/无效电平即高/低电平
*需要注意的寄存器：ARR、CNT、CCR*

- 输出PWM即使用PWM模式实现
![[Pasted image 20230801155505.png]]

- PWM参数计算
![[Pasted image 20230801155858.png]]
