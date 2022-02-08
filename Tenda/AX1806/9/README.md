Affect device: Tenda Router AX1806 v1.0.0.1(https://www.tenda.com.cn/download/detail-3306.html)

Vulnerability Type: Stack overflow

Impact: Denial of Service(DoS)

# Vulnerability description

This vulnerability lies in the `/goform/saveParentControlInfo` page which influences the lastest version of Tenda Router AX1806 v1.0.0.1: https://www.tenda.com.cn/download/detail-3306.html

There is a stack overflow vulnerability in the `saveParentControlInfo` function.

The `v3` variable is obtained directly from the http request parameter `deviceName`.

Then this function calls the setdevicename function.

![image-20220208230322319](image/1.png)

In the setdevicename function, this function uses `sprintf(... , "%s" , ...)` to copy the string pointed by `a1` into a stack buffer pointed by `v9`.

![image-20220208230537690](image/2.png)

So by POSTing the page `/goform/saveParentControlInfo` with long `deviceName`, the attacker can easily perform a Denial of Service(DoS).

# POC

Poc of Denial of Service(DoS):