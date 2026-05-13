## VLAN filtering with simplified bridge VLAN table 

**==> picture [13 x 13] intentionally omitted <==**

This issue has been resolved since RouterOS v7.15 . Dynamic VLANs are now always created as separate entries and no longer merge with statically configured ones. 

You need to create a network setup where multiple clients are connected to separate access ports and isolated by different VLANs, this traffic should be tagged and sent to the appropriate trunk port. Access ports are configured using a pvid property. As the trunk port is used on both VLANs, you decided to simplify configuration by adding a single bridge VLAN table entry and separate VLANs by a comma. This is especially useful when tagged trunk ports are used across large numbers of VLANs or even certain VLAN ranges (e.g. vlan-id=100-200). See a network diagram and configuration below. 

**==> picture [484 x 161] intentionally omitted <==**
