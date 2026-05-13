## Sub-menu: `/interface bridge msti` 

This section is used to group multiple VLAN IDs into a single instance to create a different root bridge for each VLAN group inside an MSTP region. 

**==> picture [511 x 120] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (text; Default: ) Bridge to which assigns an MST instance.<br>identifier  (integer: 1..31; Default: ) MST instance identifier.<br>priority  (integer: 0..65535 decimal format or  MST instance priority, is used to determine the root bridge for a group of VLANs in an MSTP<br>0x0000-0xffff hex format; Default: 32768 / 0x8000 ) region.<br>vlan-mapping  (integer: 1..4094; Default: ) The list of VLAN IDs to assign to MST instance. This setting accepts the VLAN ID range, as well<br>as comma, separated values. E.g.  vlan-mapping=100-115,120,122,128-130<br>**----- End of picture text -----**<br>
