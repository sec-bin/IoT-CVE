# 漏洞描述

设备：Tenda-AX1806 v1.0.0.1 https://www.tenda.com.cn/download/detail-3306.html

漏洞类型：堆溢出

攻击效果：拒绝服务

# 漏洞成因

该漏洞发生于tdhttpd文件的saveParentControlInfo函数中，goform/saveParentControlInfo页面

在该函数中，存在堆溢出漏洞

如图，v2来源于http数据包中的deviceId参数

随后，该函数调用了strcpy函数来将deviceId的数据复制到v5指向的堆区，这一过程缺少长度的安全性检测，由此引发堆溢出

![image-20220208233321867](image/1.png)

攻击者可利用这一点，通过一串长deviceId，触发堆溢出，实现拒绝服务攻击

# POC

拒绝服务poc：

