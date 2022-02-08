Affect device: Tenda Router AX1806 v1.0.0.1(https://www.tenda.com.cn/download/detail-3306.html)

Vulnerability Type: Stack overflow

Impact: Denial of Service(DoS)

# Vulnerability description

This vulnerability lies in the `/goform/fast_setting_wifi_set` page which influences the lastest version of Tenda Router AX1806 v1.0.0.1: https://www.tenda.com.cn/download/detail-3306.html



There is a stack overflow vulnerability in the `form_fast_setting_wifi_set` function.

The `v3` variable is obtained directly from the http request parameter `ssid`.

`v5` = `v3`.

Then this function uses `cmsUtl_strcpy` to copy the **variable v5 to the stack variable v34** without any sercuity check.

![image-20220208210113892](image/1.png)

Let's look at the `cmsUtl_strcpy` function. It only checks the null pointer case, and directly calls the strcpy function without checking the length of the copied string, which causes a **stack overflow**.

![image-20220208210447517](image/2.png)

So by POSTing the page `/goform/fast_setting_wifi_set` with long `ssid`, the attacker can easily cause a **Deny of Service(DoS)**.

# POC

poc to DoS:

