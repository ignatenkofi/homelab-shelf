## Egress VLAN Tag 

Egress packets can be assigned different VLAN tag formats. The VLAN tags can be removed, added, or remained as is when the packet is sent to the egress port (destination port). Each port has dedicated control of the egress VLAN tag format. The tag formats include: 

Untagged Tagged Unmodified 

The Egress VLAN Tag table includes 4096 entries for VLAN tagging selection. 

Sub-menu: `/interface ethernet switch egress-vlan-tag` 

**==> picture [287 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Enables or disables Egress VLAN Tag table entry.<br>tagged-ports  (ports) Ports that are tagged in egress.<br>vlan-id  (0..4095) VLAN ID which is tagged in egress.<br>**----- End of picture text -----**<br>
