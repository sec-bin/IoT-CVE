# 漏洞描述

设备：Tenda-AX1806 v1.0.0.1 https://www.tenda.com.cn/download/detail-3306.html

漏洞类型：堆溢出

攻击效果：拒绝服务

# 漏洞成因

该漏洞发生于tdhttpd文件的saveParentControlInfo函数中，goform/saveParentControlInfo页面

在该函数中，存在堆溢出漏洞

![image-20220209002024781](image/1.png)

首先，该函数会调用sub_60CFC函数，注意传入的参数v6是一个堆地址指针

进入sub_60CFC函数，v16直接来源于http数据包中的urls参数

![image-20220209002202055](image/2.png)

随后，该函数调用了strcpy函数，将v16的诗句拷贝到a2 + 80中，这一过程缺乏安全检测

![image-20220209002333231](image/3.png)

而a2是堆地址指针，由此，可发生堆溢出

攻击者可以通过一串长urls，造成堆溢出，实现拒绝服务攻击

# POC

拒绝服务Poc：

