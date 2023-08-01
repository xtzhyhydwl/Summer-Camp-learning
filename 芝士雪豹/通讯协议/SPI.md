参考视频：【深入理解SPi通讯协议，5分钟看懂！】 https://www.bilibili.com/video/BV1F54y1M7e7/?share_source=copy_web&vd_source=1ca96e0b8c00193760c615cfbd038092


# 简介

- SPI：serial peripheral interface 串行外设接口

- 连接图
![[Pasted image 20230728090944.png]]

- 引脚定义：

SCK：时钟线
MOSI：Master Output Slave Input 主机发送从机接收
MISO：Master Input Slave Output 从机发送主机接收
SS1/2/3：地址线

# 读写数据

## 原理：SCK和MOSI/MISO协同

1. SS线确认收发从机（多数是写低电选中，具体看外设说明书）

2. 从机接收生效后，SCK上升/下降沿读取MOSI（具体看说明书）
![[Pasted image 20230728093105.png]]

3. 主机接收数据是时持续提供时钟信号，按照某种协同模式一位位读取MISO
![[Pasted image 20230728093414.png]]

4. 共有四种协同模式（看说明书选择）
![[Pasted image 20230728093130.png]]

- 与IIC不同，SPI并没有规定一帧数据有多长，完全取决于外设的需要