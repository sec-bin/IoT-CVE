# 漏洞描述

设备：Tenda-AX1806 v1.0.0.1 https://www.tenda.com.cn/download/detail-3306.html

漏洞类型：栈溢出

攻击效果：拒绝服务

# 漏洞成因

该漏洞发生于tdhttpd文件的formSetProvince函数中，goform/SetProvinceCode页面

在该函数中，存在栈溢出漏洞

在该函数中，v2直接来源于http数据包中的ProvinceCode参数，随后调用sprintf+"%s"，而缺少安全考虑

![image-20220209143635024](image/1.png)

因此攻击者可以通过一串长ProvinceCode来触发栈溢出，从而实现拒绝服务攻击

# POC

拒绝服务的Poc：

