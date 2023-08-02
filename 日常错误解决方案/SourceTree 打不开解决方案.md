- 想把学习笔记同步到git，发现sourcetree.exe没有反应，于是上网找到了解决方案，参考网址：[win10突然打不开sourcetree - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/637566727)

- 以下解决方案电脑版本win11实测有效

# 1. 查找错误

- 打开C:\Users\User\AppData\Local\Atlassian\SourceTree下sourcetree.log文件，ctrl+f查找当前日期，格式为“2023-08-01”
- 找到错误为"Unable to load MEF components"

![[Pasted image 20230801122728.png]]

# 2. 解决问题

- 参考网址：[Solved: SourceTree won't start - Unable to load MEF compo... (atlassian.com)](https://community.atlassian.com/t5/Sourcetree-questions/SourceTree-won-t-start-Unable-to-load-MEF-components/qaq-p/2388773)
- 根据大佬提供的解决方案，退回Atlassian，选择另一个文件夹
![[Pasted image 20230801122933.png]]
- 点进去，找到这两个文件，删除
![[Pasted image 20230801123131.png]]

- 成功运行（但是需要重新配置？）

# 3. 总结

- 闲着没事不要乱更新电脑系统