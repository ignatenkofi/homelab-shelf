## Sub-menu: `/interface bridge port mst-override` 

This section is used to select the desired path for each VLAN mapping inside an MSTP region. 

**==> picture [511 x 139] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Whether the entry is disabled.<br>internal-path-cost  (integer: 1.. Path cost for an MST instance's VLAN mapping, used on VLANs that are facing towards the root bridge to<br>200000000; Default: ) manipulate path selection, lower path cost is preferred.<br>identifier  (integer: 1..31; Default: ) MST instance identifier.<br>priority  (integer: 0..240; Default: 128 The priority of an MST instance's VLAN, used on VLANs that are facing away from the root bridge to manipulate<br>) path selection, lower priority is preferred.<br>interface  (name; Default: ) Name of the port on which use configured MST instance's VLAN mappings and defined path cost and priority.<br>**----- End of picture text -----**<br>
