## Sub-menu: `/interface bridge host` 

**==> picture [383 x 118] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (name; Default: none ) The bridge interface to which the MAC address is going to be assigned.<br>disabled  (yes | no; Default: no ) Disables/enables static MAC address entry.<br>interface  (name; Default: none ) Name of the interface.<br>mac-address  (MAC address; Default: ) MAC address that will be added to the host table statically.<br>vid  (integer: 1..4094; Default: ) VLAN ID for the statically added MAC address entry.<br>**----- End of picture text -----**<br>


For example, if it was required that all traffic destined to 4C:5E:0C:4D:12:43 is forwarded only through ether2 , then the following commands can be used: 

```
/interface bridge host
add bridge=bridge interface=ether2 mac-address=4C:5E:0C:4D:12:43
```
