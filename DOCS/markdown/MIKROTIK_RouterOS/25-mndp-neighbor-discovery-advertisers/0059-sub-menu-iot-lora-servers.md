## Sub-menu: `/iot lora servers` 

There are a few predefined servers that can be used (it requires to make an The Things Network account to use them): 

```
[admin@MikroTik] /iot/lora/servers/print
Columns: NAME, UP-PORT, DOWN-PORT, ADDRESS
#  NAME              UP-PORT  DOWN-PORT  ADDRESS
0  TTS Cloud (eu1)      1700       1700  eu1.cloud.thethings.industries
1  TTS Cloud (nam1)     1700       1700  nam1.cloud.thethings.industries
2  TTS Cloud (au1)      1700       1700  au1.cloud.thethings.industries
3  TTN V3 (eu1)         1700       1700  eu1.cloud.thethings.network
4  TTN V3 (nam1)        1700       1700  nam1.cloud.thethings.network
5  TTN V3 (au1)         1700       1700  au1.cloud.thethings.network
```

Custom servers can be added as well. Data forwarding to multiple servers can work simultaneously if the first server does not change "DevAdress" part of the packet and under the condition that all servers are able to decode the packet. 

**==> picture [516 x 430] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (domain  Defines LoRaWAN Network server address.<br>name or IP address;<br>Default: )<br>name  (string;  Defines server name.<br>Default: )<br>protocol  (UDP |  Specify whether to use UDP, LNS or CUPS protocol for the communication with the LoRaWAN server.<br>LNS | CUPS;<br>Default:  UDP )<br>down-port  (integer  Parameter that is used when UDP protocol is selected. Defines port for down-link communication (from server to node) with<br>[0..65535]; Default:  LoRaWAN Network server. Most of known open source servers uses port 1700 as default, but it can change if multiple servers<br>1700 ) are configured on the same machine.<br>up-port  (integer [0.. Parameter that is used when UDP protocol is selected. Defines port for up-link communication (from node to server) with<br>65535]; Default:  1700 LoRaWAN Network server. Most of known open source servers uses port 1700 as default, but it can change if multiple servers<br>) are configured on the same machine.<br>netid  (list of string;  Parameter that is used when UDP protocol is selected. Applies a filter to only send LoRaWAN payloads that match the Network<br>Default: ) ID (Net ID) filter configured.<br>joineui  (list of string; Parameter that is used when UDP protocol is selected. Applies a filter to only send LoRaWAN payloads that match the Join EUI<br>Default: ) filter configured.<br>port  (integer [0.. Parameter that is used when LNS or CUPS protocol is selected. For LNS, defines the WSS (WebSocket) port and, for CUPS,<br>65535]; Default:  8887 defines HTTPS port.<br>)<br>key  (string; Default:  Parameter that is used when LNS or CUPS protocol is selected. Specify the LoRa Basics Station LNS Authentication Key or<br>) CUPS API KEY (both generated on the server).<br>ssl  (yes or no;  Parameter that is used when LNS or CUPS protocol is selected. Specify whether to use or not to use SSL (if the server supports<br>Default: no) TLS server authentication). When this option is choosen, root SSL certificate(s) must be uploaded under the certificates menu.<br>certificate  (list of  Parameter that is used when LNS or CUPS protocol is selected. Select an uploaded client certificate (if the server awaits TLS<br>string; Default:  none ) client authentication). If TLS client authentication is not required by the server, use the default " none " setting.<br>interval  (integer [0.. Parameter that is used when CUPS protocol is selected. Specify the interval with which the LoRa Basics Station will query CUPS<br>65535]; Default: ) server for configuration updates/changes.<br>**----- End of picture text -----**<br>


There are a few pre-configued The Things default servers. If you deleted one and want to recover default servers, you can use the command: 

```
/iot lora server reset-servers
```

1604 

**==> picture [13 x 13] intentionally omitted <==**

Please be warned that resetting servers will delete all previously configured servers as well, so make sure to "save" them beforehand.
