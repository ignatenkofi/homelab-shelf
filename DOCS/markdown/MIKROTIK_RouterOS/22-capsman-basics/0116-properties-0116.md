## Properties 

**==> picture [504 x 158] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>3gpp  (string; Default: )<br>area-prefix  (string;  Rule matches if area value of AP (a proprietary extension) begins with specified value. area value is a proprietary extension.<br>Default: )<br>comment  (string;  Short description of an entry<br>Default: )<br>connect  (yes | no;  Available options:<br>Default: yes )<br>yes - Connect to access point that matches this rule.<br>no - Do not connect to any access point that matches this rule.<br>**----- End of picture text -----**<br>


1402 

disabled (yes | no; Default: no ) mac-address (MAC; Rule matches only AP with the specified MAC address. Value 00:00:00:00:00:00 matches always. Default: 00:00:00:00: 00:00 ) security-profile (string Name of security profile that is used when connecting to matching access points, If value of this property is none, then | none; Default: none ) security profile specified in the interface configuration will be used. In station mode, rule will match only access points that can support specified security profile. Value none will match access point that supports security profile that is specified in the interface configuration. In access point mode value of this property will not be used to match remote devices. signal-range (NUM.. Rule matches if signal strength of the access point is within the range. If station establishes connection to access point that NUM - both NUM are is matched by this rule, it will disconnect from that access point when signal strength goes out of the specified range. numbers in the range -120..120; Default: -12 0..120 ) ssid (string; Default: "" ) Rule matches access points that have this SSID. Empty value matches any SSID. This property has effect only when station mode interface ssid is empty, or when access point mode interface has wds-ignore-ssid =yes wireless-protocol (802. 11 | any | nstreme | tdma; Default: any ) interface (string; Each rule in connect list applies only to one wireless interface that is specified by this setting. Default: )
