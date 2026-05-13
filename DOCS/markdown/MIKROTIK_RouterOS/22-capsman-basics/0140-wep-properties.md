## WEP properties 

These properties have effect only when mode is set to static-keys-required or static-keys-optional. 

**==> picture [504 x 185] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>static-key-0 | static-key-1 |  Hexadecimal representation of the key. Length of key must be appropriate for selected algorithm. See the Statically<br>static-key-2 | static-key-3  (h configured WEP keys section.<br>ex; Default: )<br>static-algo-0 | static-algo-1  Encryption algorithm to use with the corresponding key.<br>| static-algo-2 | static-algo-3<br>(none | 40bit-wep | 104bit-<br>wep | tkip | aes-ccm;<br>Default: none )<br>static-transmit-key  (key-0 |  Access Point will use the specified key to encrypt frames for clients that do not use private key. Access Point will also<br>key-1 | key-2 | key-3;  use this key to encrypt broadcast and multicast frames. Client will use the specified key to encrypt frames if  static-sta-<br>Default: key-0 ) private-algo is set to none. If corresponding static-algo-N property has value set to none, then frame will be sent<br>unencrypted (when mode is set to static-keys-optional) or will not be sent at all (when mode is set to static-keys-<br>required).<br>**----- End of picture text -----**<br>


1416 

static-sta-private-key (hex; Length of key must be appropriate for selected algorithm, see the Statically configured WEP keys section. This Default: ) property is used only on Stations. Access Point uses corresponding key either from private-key property, or from Mikro tik-Wireless-Enc-Key attribute. static-sta-private-algo (none Encryption algorithm to use with station private key. Value none disables use of the private key. This property is only | 40bit-wep | 104bit-wep | used on Stations. Access Point has to get corresponding value either from private-algo property, or from Mikrotiktkip | aes-ccm; Default: none Wireless-Enc-Algo attribute. Station private key replaces key 0 for unicast frames. Station will not use private key to ) decrypt broadcast frames.
