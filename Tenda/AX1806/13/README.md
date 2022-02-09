Affect device: Tenda Router AX1806 v1.0.0.1(https://www.tenda.com.cn/download/detail-3306.html)

Vulnerability Type: Stack overflow

Impact: Denial of Service(DoS)

# Vulnerability description

This vulnerability lies in the `/goform/SetProvinceCode` page which influences the lastest version of Tenda Router AX1806 v1.0.0.1: https://www.tenda.com.cn/download/detail-3306.html

There is a stack overflow vulnerability in the `formSetProvince` function.

The `v2` variable is obtained directly from the http request parameter `ProcinceCode`.

Then this function uses `sprintf(... , "%s" , ...)` to copy the string pointed by `v2` into a stack buffer pointed by `s`.

![image-20220209143635024](image/1.png)

So it caused stack overflow, by POSTing the page `/goform/SetProvinceCode` with long `ProvinceCode`, the attacker can easily perform a 

Denial of Service(DoS).

# POC

Poc of Denial of Service(DoS):