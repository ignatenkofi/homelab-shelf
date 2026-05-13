## Port isolation 

Since RouterOS v6.43 is it possible to create a Private VLAN setup, an example can be found in the Switch chip port isolation manual page. Hardware offloaded bonding interfaces are not included in the switch port-isolation menu, but it is still possible to configure port-isolation individually on each secondary interface of the bonding. 

**==> picture [13 x 13] intentionally omitted <==**

Port isolation can be used with vlan-filtering bridge and it is possible to isolate ports that are members of the same VLAN. The isolation works per-port, it is not possible to isolate ports per-VLAN.
