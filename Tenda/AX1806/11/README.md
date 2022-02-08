Affect device: Tenda Router AX1806 v1.0.0.1(https://www.tenda.com.cn/download/detail-3306.html)

Vulnerability Type: Heap overflow

Impact: Denial of Service(DoS)

# Vulnerability description

This vulnerability lies in the `/goform/saveParentControlInfo` page which influences the lastest version of Tenda Router AX1806 v1.0.0.1: https://www.tenda.com.cn/download/detail-3306.html

There is a heap overflow vulnerability in the `saveParentControlInfo` function.

![image-20220209002024781](image/1.png)

Firstly, this function calls the sub_60CFC function and the second parameter v6 is a heap address pointer.

![image-20220209002202055](image/2.png)

In the sub_60CFC function, the `v16` variable is obtained directly from the http request parameter `urls`.

Then this function will use the strcpy function to copy the v16 to a2 + 80.

![image-20220209002333231](image/3.png)

However, a2 is a heap address pointer.So it causes heap overflow.

So by POSTing the page `/goform/saveParentControlInfo` with long `urls`, the attacker can easily perform a Denial of Service(DoS).

# POC

Poc of Denial of Service(DoS):