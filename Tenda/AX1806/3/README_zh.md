设备：Tenda-AX1806 v1.0.0.1 https://www.tenda.com.cn/download/detail-3306.html

漏洞类型：栈溢出

攻击效果：拒绝服务

# 漏洞成因

该漏洞发生于tdhttpd文件的`form_fast_setting_wifi_set`函数中，`/goform/fast_setting_wifi_set`页面



如图所示，v3是直接来自于http数据包中的ssid参数的，v5=v3，而随后，该函数直接调用了cmsUtl_strcpy函数来对字符串进行拷贝，拷贝到v34，其中并未对长度有任何检查

![image-20220208210113892](image/1.png)

再来看看cmsUtl_strcpy函数，该函数仅仅只对空指针的情况做了检查，而对被拷贝的字符串的长度没有任何的检查措施，由此造成了栈溢出

![image-20220208210447517](image/2.png)

因此，通过设置较长的ssid，攻击者可以利用这一点造成拒绝服务攻击

# POC

拒绝服务的Poc：

