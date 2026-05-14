## AAA properties 

Properties in this category configure an access point's interaction with AAA (RADIUS) servers. 

Certain parameters in the table below take format-string as their value. In a format-string, certain characters are interpreted in the following way: 

**==> picture [347 x 137] intentionally omitted <==**

**----- Start of picture text -----**<br>
Character Interpretation<br>a Hexadecimal character making up the MAC address of the client device in lowercase<br>A Hexadecimal character making up the MAC address of the client device in upper case<br>i Hexadecimal character making up the MAC address of the AP's interface in lowercase<br>I (capital 'i')  Hexadecimal character making up the MAC address of the AP's interface in upper case<br>N The entire name of the AP's interface (e.g. 'wifi1')<br>S The entire SSID<br>**----- End of picture text -----**<br>

All other characters are used without interpreting them in any way. For examples, see default values. 

**==> picture [516 x 267] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>called-format  (format-string; Default:  II-II- Format for the value of the Called-Station-Id RADIUS attribute, in AP's messages to RADIUS servers.<br>II-II-II-II:S )<br>calling-format  (format-string; Default:  AA: Format for the value of the Calling-Station-Id RADIUS attribute, in AP's messages to RADIUS servers.<br>AA:AA:AA:AA:AA )<br>interim-update  (time interval; Default:  5m ) Interval at which to send interim updates about traffic accounting to the RADIUS server.<br>mac-caching  (time interval; Default:  disabl Length of time to cache RADIUS server replies, when MAC address authentication is enabled.<br>ed ) This resolves issues with client device authentication timing out due to (comparatively high latency of<br>RADIUS server replies.<br>name  (string; Default:  no ) A unique name for the AAA profile.<br>nas-identifier  (string)  Value of the NAS-Identifier attribute, in AP's messages to RADIUS servers. Defaults to the host name of<br>the device (/system/identity).<br>password-format  (format-string) Format for value to use in calculating the value of the User-Password attribute in AP's messages to<br>RADIUS servers when performing MAC address authentication.<br>Default value: "" (an empty string).<br>username-format  (format-string; Default:  A Format for the value of the User-Name attribute in APs messages to RADIUS servers when performing<br>A:AA:AA:AA:AA:AA ) MAC address authentication.<br>**----- End of picture text -----**<br>
