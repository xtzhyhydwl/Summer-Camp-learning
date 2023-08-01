- 参考视频：【4分钟看懂！I2C通讯协议 最简单的总线通讯！】 https://www.bilibili.com/video/BV1dg4y1H773/?share_source=copy_web&vd_source=1ca96e0b8c00193760c615cfbd038092

# 简介

- IIC/I2C : inter-intergrated circuit 设备间（集成电路）通讯

![[Pasted image 20230727211933.png]]

- 一主多从模式

![[Pasted image 20230727212201.png]]

# 读写数据

## 原理：由SCL和SDA协同读取/写入

## 时序：

1. 标准数据帧（定型文）

![[Pasted image 20230727212852.png]]

2. SCL、SDA高低电平对应位

![[Pasted image 20230727213754.png]]

- 注意应答信号的1，表示主机读取完成时，是由主机发送给从机！其他情况下都是从机发送给主机。