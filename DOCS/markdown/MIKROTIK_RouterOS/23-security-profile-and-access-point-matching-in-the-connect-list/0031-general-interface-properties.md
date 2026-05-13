## General interface properties 

Sub-menu: `/interface w60g` 

**==> picture [13 x 13] intentionally omitted <==**

Wireless Wire kit devices comes in pre-configured, connected pairs. Manual configuration is optional 

**==> picture [516 x 206] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>arp  (disabled | enabled | proxy-arp | reply-only;  Read more >><br>Default:  enabled )<br>arp-timeout  (auto | integer; Default:  auto ) ARP timeout is time how long ARP record is kept in ARP table after no packets are received from<br>IP. Value  auto  equals to the value of  arp-timeout  in  /ip settings , default is 30s<br>comment  (string; Default: ) Short description of the interface<br>disabled  (yes | no; Default:  yes ) Whether interface is disabled<br>frequency  (58320 | 60480 | 62640 | 64800 | 66000 |  Frequency used in communication (Only active on bridge device)<br>auto; Default:  auto )<br>isolate-stations  (yes | no; Default:  yes ) Don't allow communication between connected clients (from RouterOS 6.41)<br>l2mtu  (integer [0..7882]; Default:  1600 ) Layer2 Maximum transmission unit<br>mac-address  (MAC; Default: ) MAC address of the radio interface<br>**----- End of picture text -----**<br>


1427 

**==> picture [516 x 242] intentionally omitted <==**

**----- Start of picture text -----**<br>
mdmg-fix  (yes | no; Default:  no ) Experimental feature working only on wAP60Gx3 devices, providing better point to multi point<br>stability in some cases<br>mode  (ap-bridge | bridge | sniff | station-bridge;  Operation mode<br>Default:  bridge )<br>mtu  (integer [32..8192]; Default:  1500 ) Layer3 Maximum transmission unit<br>name  (string; Default:  wlan60-1 ) Name of the interface<br>password  (string; Default:  randomly generated ) Password used for AES encryption<br>put-stations-in-bridge  (; Default: ) Put newly created station device interfaces in this bridge<br>region  (asia | australia | canada | china | eu | japan |  Parameter to limit frequency use<br>no-region-set | usa; Default:  no-region-set )<br>scan-list  (58320,60480,62640,64800,66000;  Scan list to limit connectivity over frequencies in station mode<br>Default:  58320,60480,62640,64800 )<br>ssid  (string (0..32 chars); Default:  value of System  SSID (service set identifier) is a name that identifies wireless network<br>Identity )<br>tx-sector  (integer [0..63] | auto; Default:  auto ) Disables beamforming and locks to selected radiation pattern<br>**----- End of picture text -----**<br>
