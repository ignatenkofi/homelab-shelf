## Script repository 

Sub-menu level: `/system script` 

Contains all user-created scripts. Scripts can be executed in several different ways: 

on event - scripts are executed automatically on some facility events ( scheduler, netwatch, VRRP) by another script - running script within the script is allowed manually - from console executing a run command or in winbox 

**==> picture [13 x 13] intentionally omitted <==**

Only scripts (including schedulers, netwatch, etc) with equal or higher permission rights can execute other scripts. 

**==> picture [13 x 13] intentionally omitted <==**

When executing script from GUI or CLI, user permissions are used. To run a script with script permissions, a script must be executed from CLI with additional "use-script-permissions" parameter. 

**==> picture [509 x 251] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>comment  (string; Default: ) Descriptive comment for the script<br>dont-require-permissions  (yes | no; Default: no) Bypass permissions check when the script is being executed, useful when scripts are being<br>executed from services that have limited permissions, such as Netwatch<br>name  (string; Default: "Script[num]") name of the script<br>policy  (string; Default: ftp,reboot,read,write,policy, list of applicable policies:<br>test,password,sniff,sensitive,romon)<br>ftp  - can log on remotely via FTP and send and retrieve files from the router<br>password  - change passwords<br>policy  - manage user policies, add and remove user<br>read  - can retrieve the configuration<br>reboot  - can reboot the router<br>sensitive  - allows changing "hide sensitive" parameter<br>sniff  - can run sniffer, torch, etc<br>test  - can run ping, traceroute, bandwidth test<br>write  - can change the configuration<br>Read more detailed policy descriptions here<br>source  (string;) Script source code<br>**----- End of picture text -----**<br>


Read-only status properties: 

**==> picture [300 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>last-started  (date) Date and time when the script was last invoked.<br>owner  (string) The user who created the script<br>run-count  (integer) Counter that counts how many times the script has been executed<br>**----- End of picture text -----**<br>


Menu specific commands 

1110 

**==> picture [315 x 62] intentionally omitted <==**

**----- Start of picture text -----**<br>
Command Description<br>run  (run [id|name]) Execute the specified script by ID or name using user permissions.<br>use-script-permissions Additional parameter to execute script using script permissions.<br>**----- End of picture text -----**<br>
