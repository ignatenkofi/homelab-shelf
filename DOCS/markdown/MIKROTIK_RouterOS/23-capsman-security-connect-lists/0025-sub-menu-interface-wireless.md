## Sub-menu: `/interface wireless` 

With VLAN tagging it is possible to separate Virtual AP traffic on Ethernet side of "locally forwarding" AP (the one on which wireless interfaces are bridged with Ethernet). This is necessary to separate e.g. "management" and "guest" network traffic of Ethernet side of APs. 

VLAN is assigned for wireless interface and as a result all data coming from wireless gets tagged with this tag and only data with this tag will send out over wireless. This works for all wireless protocols except that on Nv2 there's no Virtual AP support. 

You can configure your RADIUS authentication server to assign users or groups of users to a specific VLAN when they authenticate to the network. To use this option you will need to use RADIUS attributes. 

Note: In case to use this option you must enable wireless-fp or wireless-cm2 package for RouterOS version up to 6.37. Starting from RouterOS v6.37 you can do that with regular wireless package. 

1425 

**==> picture [400 x 109] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>vlan-mode  (no tag | user service tag | use tag; Default: no tag ) Three VLAN modes are available:<br>no-tag - AP don't use VLAN tagging<br>use-service-tag - VLAN ID use 802.1ad tag type<br>use-tag - VLAN ID use 802.1q tag type<br>vlan-id  (integer [1..4095]; Default: 1 ) VLAN identification number<br>**----- End of picture text -----**<br>
