## Introduction 

Mangle is a kind of 'marker' that marks packets for future processing with special marks. Many other facilities in RouterOS make use of these marks, e.g. queue trees, NAT, routing. They identify a packet based on its mark and process it accordingly. The mangle marks exist only within the router, they are not transmitted across the network. 

Additionally, the mangle facility is used to modify some fields in the IP header, like TOS (DSCP) and TTL fields. 

Firewall mangle rules consist of five predefined chains that cannot be deleted: 

**==> picture [504 x 173] intentionally omitted <==**

The PREROUTING chain: Rules in this chain apply to packets as they just arrive on the network interface; The INPUT chain: Rules in this chain apply to packets just before they’re given to a local process; The OUTPUT chain: The rules here apply to packets just after they’ve been produced by a process; The FORWARD chain: The rules here apply to any packets that are routed through the current host; The POSTROUTING chain: The rules in this chain apply to packets as they just leave the network interface;
