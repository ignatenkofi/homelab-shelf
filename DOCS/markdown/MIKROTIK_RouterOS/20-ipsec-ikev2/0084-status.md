## Status 

Command `/interface pppoe-client monitor` will display current PPPoE status. 

Available read only properties: 

**==> picture [405 x 289] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>ac-mac  (MAC address) MAC address of the access concentrator (AC) the client is connected to<br>ac-name  (string) name of the Access Concentrator<br>active-links  (integer) Number of bonded MLPPP connections, ('1' if not using MLPPP)<br>encoding  (string) encryption and encoding (if asymmetric, separated with '/') being used in this connection<br>local-address  (IP Address) IP Address allocated to client<br>remote-address  (IP Address) Remote IP Address allocated to server (ie gateway address)<br>mru  (integer) effective MRU of the link<br>mtu  (integer) effective MTU of the link<br>service-name  (string) used service name<br>status  (string) current link status. Available values are:<br>dialing,<br>verifying password...,<br>connected,<br>disconnected.<br>uptime  (time) connection time displayed in days, hours, minutes and seconds<br>**----- End of picture text -----**<br>
