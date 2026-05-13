## Properties 

**==> picture [516 x 166] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address-pool  (string | static-only;  IP pool, from which to take IP addresses for the clients. If set to static-only , then only clients that have a static<br>Default: static-only ) lease (added in the lease submenu) will be allowed.<br>code  (integer:1..254; Default: ) DHCP option code. All codes are available at http://www.iana.org/assignments/bootp-dhcp-parameters<br>comment  (string; Default: ) Short description of option matcher.<br>disabled  (yes | no; Default: no ) Whether an item is disabled<br>matching-type  (exact | substring;  Matching method:<br>Default: )<br>exact - option should match exactly to value;<br>substring - value can match anywhere in the option string — at the start, middle, or end.<br>**----- End of picture text -----**<br>


902 

**==> picture [516 x 144] intentionally omitted <==**

**----- Start of picture text -----**<br>
name  (string; Default: ) Descriptive name for option matcher.<br>option-set  (name | none; Default: no A custom set of DHCP options defined in the Option Sets menu.<br>ne )<br>server  (string all|  ; Default: ) Server name which serves option matcher.<br>value  (string; Default: ) A value that will be searched for in option.<br>Available data types for value are:<br>string;<br>HEX.<br>**----- End of picture text -----**<br>
