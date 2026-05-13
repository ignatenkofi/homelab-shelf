## Bridge VLAN table 

372 

Bridge VLAN table represents per-VLAN port mapping with an egress VLAN tag action. The `tagged` ports send out frames with a corresponding VLAN ID tag. The `untagged` ports remove a VLAN tag before sending out frames. Bridge ports with `frame-types` set to `admit-all` or `admitonly-untagged-and-priority-tagged` will be automatically added as untagged ports for the `pvid` VLAN. 

Sub-menu: `/interface bridge vlan` 

**==> picture [502 x 226] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (name; Default: n The bridge interface which the respective VLAN entry is intended for.<br>one )<br>disabled  (yes | no;  Enables or disables Bridge VLAN entry.<br>Default: no )<br>tagged  (interfaces;  Interfaces or interface list with a VLAN tag adding action in egress. This setting accepts comma-separated values. e.g. ta<br>Default: none ) gged=ether1,ether2 .<br>untagged  (interfaces;  Interfaces or interface list with a VLAN tag removing action in egress. This setting accepts comma-separated values. e.g.<br>Default: none ) untagged=ether3,ether4.<br>vlan-ids  (integer 1..4094 The list of VLAN IDs for certain port configuration. This setting accepts the VLAN ID range as well as comma-separated<br>; Default: 1 ) values. e.g. vlan-ids=100-115,120,122,128-130 .<br>The vlan-ids parameter can be used to specify a set or range of VLANs, but specifying multiple VLANs in a single bridge VLAN table<br>entry should only be used for ports that are tagged ports. In case multiple VLANs are specified for access ports, then tagged packets might<br>get sent out as untagged packets through the wrong access port, regardless of the PVID value.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Make sure you have added all needed interfaces to the bridge VLAN table when using bridge VLAN filtering. For routing functions to work properly on the same device through ports that use bridge VLAN filtering, you will need to allow access to the bridge interface (this automatically include a switch-cpu port when HW offloaded vlan-filtering is used, e.g. on CRS3xx series switches), this can be done by adding the bridge interface itself to the VLAN table, for tagged traffic you will need to add the bridge interface as a tagged port and create a VLAN interface on the bridge interface. Examples can be found in the inter-VLAN routing and Management port sections. 

**==> picture [13 x 13] intentionally omitted <==**

When allowing access to the CPU, you are allowing access from a certain port to the actual router/switch, this is not always desirable. Make sure you implement proper firewall filter rules to secure your device when access to the CPU is allowed from a certain VLAN ID and port, use firewall filter rules to allow access to only certain services. 

**==> picture [13 x 13] intentionally omitted <==**

Improperly configured bridge VLAN filtering can cause security issues, make sure you fully understand how Bridge VLAN table works before deploying your device into production environments.
