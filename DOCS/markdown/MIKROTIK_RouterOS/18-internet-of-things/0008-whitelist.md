## Whitelist 

In this tab, it is possible to configure a whitelist that is going to be used in the filter policy in the "Scanners" section. In other words, an option to specify which Bluetooth addresses are going to be scanned (displayed in the "Advertising reports"). 

You can view the whitelisted entries with the command: 

```
/iot bluetooth whitelist print
Columns: DEVICE, ADDRESS-TYPE, ADDRESS
# DEVICE  ADDRESS-TYPE  ADDRESS
0 bt1     any           *:*:*:*:*:*
```

You can add a new whitelist entry with the command: 

```
/iot bluetooth whitelist add
```
