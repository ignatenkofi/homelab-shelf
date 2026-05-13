## Configurable properties: 

**==> picture [516 x 181] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (MAC address; Default: ) Advertiser's address<br>address-type  (any | public | random; Default: ) Advertiser's address type<br>comment  (string; Default: ) Short description of the whitelisted entry<br>copy-from An option to copy an entry - for more information check the console documentation<br>device  (bt1; Default: ) Select the Bluetooth interface/chip name<br>disabled  (yes | no; Default: ) An option to disable or to enable the entry<br>Only 8 whitelisted entries can be added prior to  7.14beta8  version.<br>Starting with  7.14beta8  version, whitelist is no longer limited to 8 entries and address field supports asterisk wildcards.<br>**----- End of picture text -----**<br>


If, for example, you want to whitelist all MAC addresses that begin with "DC:2C:..." octets, add an entry using wildcard asterisk characters: 

```
/iot bluetooth whitelist add address=DC:2C:*:*:*:*
```

Wildcard asterisk can not be used in-between specific octets, like " `AA:*:*:BB:*:*` " (it is an invaldi entry). 

Valid entries would be: 

```
AA:BB:CC:DD:*:*
```

```
AA:BB:CC:DD:EE:*
AA:*:*:*:*:*
```

1561
