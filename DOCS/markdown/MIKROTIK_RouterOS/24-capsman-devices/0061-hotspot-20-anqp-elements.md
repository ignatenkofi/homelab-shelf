## Hotspot 2.0 ANQP elements 

Hotspot 2.0 specification introduced some additional ANQP elements. These elements use an ANQP vendor specific element ID. Here are available properties to change these elements. 

**==> picture [504 x 406] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>hotspot20  (yes | no; Default: yes ) Indicate Hotspot 2.0 capability of the Access Point.<br>hotspot20-dgaf  (yes | no; Default: yes ) Downstream Group-Addressed Forwarding (DGAF). Sets value of DGAF bit to indicate whether multicast<br>and broadcast frames to clients are disabled or enabled.<br>yes  - multicast and broadcast frames to clients are enabled;<br>no  - multicast and broadcast frames to clients are disabled.<br>To disable multicast and broadcast frames set multicast-helper=full .<br>operational-classes  (list of numbers;  Information about other available bands of the same ESS.<br>Default: )<br>operator-names  (string:lang; Default:  Set operator name. Language must be specified for each operator name entry.<br>) Operator-names parameter consists of zero or more duple that contain Operator Name and Language Code:<br>operator-names=BestOperator:eng,MejorOperador:es<br>The Language Code field value is a two or three-character 8 language code selected from ISO-639.<br>wan-at-capacity  (yes | no; Default: no ) Whether the Access Point or the network is at its max capacity. If set to yes no additional mobile devices<br>will be permitted to associate to the AP.<br>wan-downlink  (number; Default: 0 ) The downlink speed of the WAN connection set in kbps. If the downlink speed is not known, set to 0.<br>wan-downlink-load  (number; Default: 0 The downlink load of the WAN connection measured over wan-measurement-duration . Values from 0<br>) to 255.<br>0  - unknown;<br>255  - 100%.<br>wan-measurement-duration  (number;  Duration during which wan-downlink-load and wan-uplink-load are measured. Value is a numeric value<br>Default: 0 ) from 0 to 65535 representing tenths of seconds.<br>0  - not measured;<br>10  - 1 second;<br>65535  - 1 hour 49 minutes or more.<br>**----- End of picture text -----**<br>


1512 

**==> picture [504 x 125] intentionally omitted <==**

**----- Start of picture text -----**<br>
wan-status  (down | reserved | test |  Information about the status of the Access Point's WAN connection. The value reserved is not used.<br>up; Default: reserved )<br>wan-symmetric  (yes | no; Default: no ) Weather the WAN link is symmetric (upload and download speeds are the same) or not.<br>wan-uplink  (number; Default: 0 ) The uplink speed of the WAN connection set in kbps. If the uplink speed is not known set to 0.<br>wan-uplink-load  (number; Default: 0 ) The uplink load of th WAN connection measured over wan-measurement-duration. Values from 0 to 255.<br>0  - unknown;<br>255  - 100%.<br>**----- End of picture text -----**<br>
