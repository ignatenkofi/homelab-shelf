## NTP Server settings: 

Server configuration is located in /system ntp server 

**==> picture [516 x 267] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (yes or no; default  Enable NTP server<br>value: no)<br>broadcast  (yes or no;  Enable certain NTP server mode, for this mode to work you have to set up broadcast-addresses field<br>default value: no)<br>multicast  (yes or no; default  Enable certain NTP server mode<br>value: no)<br>manycast  (yes or no; default  Enable certain NTP server mode<br>value: no)<br>broadcast-addresses  (IP  Set broadcast address to use for NTP server broadcast mode<br>address; default value: )<br>vrf  (default: main) Virtual Routing and Forwarding<br>use-local-clock  (yes or no;  The server will supply its local system time as valid if others are not available.<br>default value: no)<br>local-clock-stratum Manually set stratum if  use-local-clock=yes<br>auth-key  (default value: none) NTP symmetric key, used for authentication between the NTP client and server. Key Identifier (Key ID) - an integer<br>identifying the cryptographic key used to generate the message-authentication code.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

If you use use-local-clock, then be aware that the router's internal CPU clock is not a reliable time source for precise timing operations, as its frequency may vary due to power management, thermal conditions, and hardware differences, even between identical models. This variation is expected and does not affect normal router performance. For accurate timekeeping, it is recommended to use network-based time synchronisation, such as NTP (Network Time Protocol).
