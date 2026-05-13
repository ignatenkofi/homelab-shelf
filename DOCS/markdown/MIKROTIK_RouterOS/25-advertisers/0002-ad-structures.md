## AD structures 

This section allows you to define the payload for the advertising packets that are going to be broadcasted by the Bluetooth chip. 

Currently, only 4 types are supported: 0x08 "Shortened Local Name"; 0x09 "Complete Local Name"; 0xFF "Manufacturer Specific Data"; "Service Data" 

You can check and set "AD structures" settings with the commands: 

```
/iot bluetooth advertisers ad-structures print
Columns: NAME, TYPE, DATA
#  NAME  TYPE              DATA
0  test  short-local-name  TEST
/iot bluetooth advertisers ad-structures set
```

Configurable properties are shown below: 

**==> picture [501 x 139] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>data  (string; Default: ) Define advertising packet's AdvData part of the payload<br>name  (string; Default: ) Descriptive name of AD structure<br>type  (complete-local-name | manufacturer-data | short-local-name | service-data; Default: ) An option to set AD structure's type:<br>0x08 "Shortened Local Name"<br>0x09 "Complete Local Name"<br>0xFF "Manufacturer Specific Data"<br>0x20 "Service Data 32-bit"<br>**----- End of picture text -----**<br>


If, for example, the "Shortened Local Name" type is chosen and the "data" field is configured with "TEST" → AdvData part of the payload is going to look like this: 

05 08 54 45 53 54 (hexadecimal format) 

, where the first octet (05) shows the number of bytes to follow (5 bytes) and the second octet (08) shows the type (Shortened Local Name). 3d, 4th, 5th and 6th (and etc) octets are the "data" [54 (hex)= T (ASCII), 45 (hex)= E (ASCII), 53 (hex)= S (ASCII), 54 (hex)= T (ASCII)]. 

The same applies to the "Complete Local Name" type. Only the second octet in the AdvData payload is going to differ and will be set to 09. 

For the "Manufacturer Specific Data" type, you will need to configure the "data" field in the hexadecimal format. The second octet for this type is going to be set to FF. 

1557
