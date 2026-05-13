## Properties 

Sub-menu: `/tool/netwatch` 

**==> picture [516 x 115] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>host  (Default:"") The IP address of the server to be probed. Formats:<br>- ipv4<br>- ipv4 @ vrf<br>- ipv6<br>- ipv6 @ vrf<br>- ipv6-linklocal % interface<br>- domain name (for type=dns)<br>**----- End of picture text -----**<br>


1789 

**==> picture [516 x 389] intentionally omitted <==**

**----- Start of picture text -----**<br>
type  (icmp | tcp-conn | http-get | ht Type of the probe:<br>tp-get | dns | simple; Default:  simple - icmp - (ping-style) series of ICMP request-response with statistics<br>) - tcp-conn - test TCP connection (3-way handshake) to a server specified by IP and port<br>- http-get - do an HTTP Get request and test for a range of correct replies<br>- https-get - do an HTTP Get request and test for a range of correct replies<br>- dns - do a specified DNS query for domain name<br>- simple - simplified ICMP probe, with fewer options than "ICMP" type, used for backward compatibility with the<br>older Netwatch version<br>interval  (Default:  10s ) The time interval between probe tests<br>timeout  (Default:  3s ) Max time limit to wait for a response<br>src-address  (Default: "" ) Source IP address which the Netwatch will try to use in order to reach the host. If address is not present, then the<br>host will be considered as "down".<br>start-delay  (Default:  3s ) Time to wait before starting probe (on add, enable, or system start)<br>startup-delay  (Default:  5m ) Time to wait until starting Netwatch probe after system startup<br>up-script  (Default:"") Script to execute on the event of probe state change 'fail' --> 'OK'<br>down-script  (Default:"") Script to execute on the event of probe state change 'OK' --> 'fail'<br>test-script  (Default:"") Script to execute at the end of every probe test<br>ignore-initial-up  (no | yes ; Default:  Specifies if "Up" script should be ran if probe state change goes from `Unknown` to 'Up', used to help against false<br>no ) positives after enabling the probe, or after a reboot. "no" means that change from Unknown to Up will not be<br>ignored.<br>ignore-initial-down  (no | yes;  Specifies if "Down" script should be ran if probe state change goes from `Unknown` to 'Down'. "no" means that<br>Default:  no ) change from 'Unknown' to 'Down' will not be ignored.<br>Should be used with care, as first "Down" status won't be executed, and Down script will only be ran if<br>probe goes through "Up" > "Down" state.<br>**----- End of picture text -----**<br>


Netwatch executes scripts as *sys user, so any defined global variable in the Netwatch script will not be readable by for an example a scheduler or other users 

**==> picture [13 x 13] intentionally omitted <==**

Netwatch is limited to read,write,test,reboot script policies. If the owner of the script does not have enough permissions to execute a certain command in the script, then the script will not be executed. If the script has greater policies than read,write,test,reboot - then the script will not be executed as well, make sure your scripts do not exceed the mentioned policies. 

It is possible to disable permission checking for RouterOS scripts under /system/scripts menu. This is useful when Netwatch does not have enough permissions to execute a script, though this decreases overall security. It is recommended to assign proper permissions to a script instead.
