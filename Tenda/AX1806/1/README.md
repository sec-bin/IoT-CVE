Affect device: Tenda Router AX1806

Vulnerability Type: Stack overflow

Impact: Remote Code Execution && Denial of Service(DoS)

# Vulnerability description

This vulnerability lies in the `/goform/SetSysTimeCfg` page which influences the lastest version of Tenda Router AX1806 v1.0.0.1: https://www.tenda.com.cn/download/detail-3306.html



There is a stack buffer overflow vulnerability in the `fromSetSysTime` function.

The `v6` variable is directly retrieved from the http request parameter `time`.

Then `v6` will be splice to stack by function sscanf without any security check,which causes stack overflow.

![image-20220208175329650](image/1.png)

So by POSTing the page `/goform/SetSysTimeCfg` with proper `time`, the attacker can easily perform a **Remote Code Execution** or **Deny of Service(DoS)** with carefully crafted overflow data.

# POC

Exploit for **Remote Code Execution**: