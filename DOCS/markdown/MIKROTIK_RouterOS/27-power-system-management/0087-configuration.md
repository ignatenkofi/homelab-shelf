## Configuration 

**==> picture [516 x 134] intentionally omitted <==**

**----- Start of picture text -----**<br>
/interface detect-internet<br>Property Description<br>detect-interface-list  (interface list; Default:  none ) All interfaces in the list will be monitored by Detect Internet<br>internet-interface-list  (interface list; Default:  none ) Interfaces with state Internet will be dynamically added to this list<br>lan-interface-list  (interface list; Default:  none ) Interfaces with state Lan will be dynamically added to this list<br>wan-interface-list  (interface list; Default:  none ) Interfaces with state Wan will be dynamically added to this list<br>**----- End of picture text -----**<br>


1758 

```
[admin@MikroTik] > interface/detect-internet/print
detect-interface-list: none
lan-interface-list: none
wan-interface-list: none
internet-interface-list: none
[admin@MikroTik] > interface/detect-internet/set internet-interface-list=all wan-interface-list=all lan-
interface-list=all detect-interface-list=all
```

```
[admin@MikroTik] > interface/detect-internet/state/print
Columns: NAME, STATE, STATE-CHANGE-TIME, CLOUD-RTT
# NAME STATE STATE-CHANGE-TIME CLO
```

```
0 ether1 internet dec/22/2020 13:46:18 5ms
```

1759
