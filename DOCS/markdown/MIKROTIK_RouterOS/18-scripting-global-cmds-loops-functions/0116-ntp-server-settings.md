## NTP Server settings: 

Server configuration is located in /system ntp server 

Property Description 

1154 

**==> picture [515 x 95] intentionally omitted <==**

**----- Start of picture text -----**<br>
enabled  (yes or no; default value: no) Enable  NTP server<br>broadcast  (yes or no; default value: no) Enable certain NTP server mode, for this mode to work you have to set up broadcast-addresses field<br>multicast  (yes or no; default value: no) Enable certain NTP server mode<br>manycast  (yes or no; default value: no) Enable certain NTP server mode<br>broadcast-addresses  (IP address; default value: ) Set broadcast address to use for NTP server broadcast mode<br>**----- End of picture text -----**<br>


Example: 

Set up an NTP server for the local network that is 192.168.88.0/24 

```
/system ntp server set broadcast=yes broadcast-addresses=192.168.88.255 enabled=yes manycast=no
```
