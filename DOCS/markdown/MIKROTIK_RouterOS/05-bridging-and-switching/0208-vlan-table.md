## VLAN Table 

VLAN table specifies certain forwarding rules for packets that have a specific 802.1Q tag. Those rules are of higher priority than switch groups configured using the Bridge Hardware Offloading feature. Basically, the table contains entries that map specific VLAN tag IDs to a group of one or more ports. Packets with VLAN tags leave the switch chip through one or more ports that are set in the corresponding table entry. The exact logic that controls how packets with VLAN tags are treated is controlled by a `vlan-mode` parameter that is changeable per switch port. 

VLAN ID based forwarding takes into account the MAC addresses dynamically learned or manually added in the host table. QCA8337 and Atheros8327 switch-chips also support Independent VLAN Learning (IVL) which does the learning based on both - MAC addresses and VLAN IDs, thus allowing the same MAC to be used in multiple VLANs. 

Packets without VLAN tag are treated just as if they had a VLAN tag with port `default-vlan-id` . If `vlan-mode=check` or `vlan=mode=secure` is configured, to forward packets without VLAN tags you have to add an entry to the VLAN table with the same VLAN ID according to `default-vlan-id` . 

**==> picture [516 x 139] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (no | yes; Default: no ) Enables or disables switch VLAN entry.<br>independent-learning  (no | yes;  Whether to use shared-VLAN-learning (SVL) or independent-VLAN-learning (IVL).<br>Default: yes )<br>ports  (name; Default: none ) Interface member list for the respective VLAN. This setting accepts comma-separated values. e.g.  ports=eth<br>er1,ether2 .<br>switch  (name; Default: none ) Name of the switch for which the respective VLAN entry is intended for.<br>vlan-id  (integer: 0..4095; Default: ) The VLAN ID for certain switch port configurations.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

Devices with MT7621 , MT7531 , EN7523, RTL8367 , 88E6393X , 88E6191X , 88E6190 switch chips support HW offloaded vlan-filtering in RouterOS v7. VLAN-related configuration on the "/interface ethernet switc `h` " menu is not available.
