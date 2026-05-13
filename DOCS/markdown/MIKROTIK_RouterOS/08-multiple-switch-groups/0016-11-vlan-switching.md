## 1:1 VLAN Switching 

1:1 VLAN switching can be used to replace the regular L2 bridging for matched packets. When a packet hits a 1:1 VLAN switching table entry, the destination port information in the entry is assigned to the packet. The matched destination information in the UFDB and MFDB entry no longer applies to the packet. 

Sub-menu: `/interface ethernet switch one2one-vlan-switching` 

**==> picture [321 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>customer-vid  (0..4095; Default: 0 ) Matching customer VLAN id for 1:1 VLAN switching.<br>disabled  (yes | no; Default: no ) Enables or disables 1:1 VLAN switching table entry.<br>dst-port  (port) Destination port for matched 1:1 VLAN switching packets.<br>service-vid  (0..4095; Default: 0 ) Matching customer VLAN id for 1:1 VLAN switching.<br>**----- End of picture text -----**<br>
