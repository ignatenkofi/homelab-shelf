## Sub-menu: `/tool/romon` 

**==> picture [358 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (yes | no; Default: no ) Disable or enable RoMON feature.<br>id  (MAC address; Default: 00:00:00:00:00:00 ) MAC address to use as ID of this router.<br>secrets  (string; Default: ) List of global secrets used for RoMON message hashing.<br>**----- End of picture text -----**<br>


When RoMON is enabled without specifying ID, the ID is automatically selected: 

```
[admin@MikroTik] /tool/romon> print
     enabled: yes
          id: 00:00:00:00:00:00
     secrets:
  current-id: DC:2C:6E:9E:11:27
```

Ports that participate in RoMON network are configured in `/tool/romon/port` menu. Port list is a list of entries that match either a specific interface or interface-list. Each entry defines whether the matched interface is allowed or forbidden to participate in the RoMON network. If participation is allowed, the entry also specifies the port's cost.
