# 漏洞描述

设备：Tenda-AX1806 v1.0.0.1 https://www.tenda.com.cn/download/detail-3306.html

漏洞类型：栈溢出

攻击效果：拒绝服务

# 漏洞成因

该漏洞发生于tdhttpd文件的formSetSysToolDDNS函数中，goform/SetDDNSCfg页面



v3直接来自于http数据包中的ddnsEn参数，随后，该函数调用了strcpy函数而未对serverName参数做任何安全性检查

![image-20220208222338204](image/1.png)

因此，攻击者可以通过一长串的serverName字符，使tdhttpd进程崩溃，从而实现拒绝服务攻击

# POC

拒绝服务的poc：

