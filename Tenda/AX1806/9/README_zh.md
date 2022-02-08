# 漏洞描述

设备：Tenda-AX1806 v1.0.0.1 https://www.tenda.com.cn/download/detail-3306.html

漏洞类型：栈溢出

攻击效果：拒绝服务

# 漏洞成因

该漏洞发生于tdhttpd文件的saveParentControlInfo函数中，goform/saveParentControlInfo页面

在该函数中发生了栈溢出漏洞

v3来源于http数据包中的deviceName参数

![image-20220208230322319](image/1.png)

随后，该函数调用了setdevicename函数

在setdevicename函数中，使用了sprintf+"%s"这样的无边界限制的组合，从a1读取数据，也就是前面的devicename

所以栈溢出发生，一串长的devicename字符可以实现拒绝服务攻击

![image-20220208230537690](image/2.png)

# POC

拒绝服务的poc：

