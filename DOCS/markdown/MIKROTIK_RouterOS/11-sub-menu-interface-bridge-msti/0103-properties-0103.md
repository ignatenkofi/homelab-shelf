## Properties 

**==> picture [501 x 150] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (DNS Name | IP  A single IP address or range of IPs to add to the address list or DNS name. You can input for example,<br>address/netmask | IP-IP; Default: '192.168.0.0-192.168.1.255' and it will auto modify the typed entry to 192.168.0.0/23 on saving.<br>)<br>dynamic  (yes, no) Allows creating data entry with dynamic form.<br>list  (string; Default: ) Name for the address list of the added IP address.<br>timeout  (time; Default: ) Time after address will be removed from the address list. If the timeout is not specified, the address will be<br>stored in the address list permanently.<br>creation-time  (time; Default: ) The time when the entry was created.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

If the timeout parameter is not specified, then the address will be saved to the list permanently on the disk. If a timeout is specified, the address will be stored on the RAM and will be removed after a system's reboot.
