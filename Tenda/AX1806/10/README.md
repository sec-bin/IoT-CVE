Affect device: Tenda Router AX1806 v1.0.0.1(https://www.tenda.com.cn/download/detail-3306.html)

Vulnerability Type: Heap overflow

Impact: Denial of Service(DoS)

# Vulnerability description

This vulnerability lies in the `/goform/saveParentControlInfo` page which influences the lastest version of Tenda Router AX1806 v1.0.0.1: https://www.tenda.com.cn/download/detail-3306.html

There is a heap overflow vulnerability in the `saveParentControlInfo` function.

The `v2` variable is obtained directly from the http request parameter `deviceId`.

Then this function calls the strcpy function to copy the v2 to v5 + 2.

However, v5 is a heap address pointer.So it causes heap overflow.

![image-20220208233321867](image/1.png)

So by POSTing the page `/goform/saveParentControlInfo` with long `deviceId`, the attacker can easily perform a Denial of Service(DoS).

# POC

Poc of Denial of Service(DoS):

