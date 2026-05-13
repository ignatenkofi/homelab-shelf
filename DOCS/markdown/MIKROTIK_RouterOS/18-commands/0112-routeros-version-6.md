## RouterOS version 6 

SNTP Client properties: Client settings example: NTP Server settings: RouterOS version 7 NTP Client properties: NTP Server settings: Log messages 

RouterOS v6 implements the SNTP protocol defined in RFC4330, manycast mode is not supported. SNTP client is included in the system package. To use an NTP server, ntp package must be installed and enabled. 

RouterOS v7 main package includes NTP client and server functionality, which is based on RFC5905. 

The client configuration is located in the /system ntp client console path, and the "System > SNTP Client" (RouterOS version 6), "System > NTP Client" (RouterOS version 7) WinBox window. This configuration is shared by the SNTP client implementation in the system package and the NTP client implementation in the ntp package. When ntp package is installed and enabled, the SNTP client is disabled automatically.
