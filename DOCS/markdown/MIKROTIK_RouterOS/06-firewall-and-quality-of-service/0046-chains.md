## Chains 

RouterOS consist of a few default chains. These chains allow you to filter packets at various points: 

- The PREROUTING chain: Rules in this chain apply to packets as they just arrive on the network interface. This chain is present in the nat, mangle and raw tables. 

- The INPUT chain: Rules in this chain apply to packets just before they’re given to a local process. This chain is present in the mangle and filter tables. 

- The OUTPUT chain: The rules here apply to packets just after they’ve been produced by a process. This chain is present in the raw, mangle, nat, and filter tables. 

- The FORWARD chain: The rules here apply to any packets that are routed through the current host. This chain is only present in the mangle and fi lter tables. 

- The POSTROUTING chain: The rules in this chain apply to packets as they just leave the network interface. This chain is present in the nat and m angle tables. 

Each of the prerouting, input, forward, output, and postrouting blocks contains even more facilities, which are illustrated in the third part of the packet flow diagram: 

670 

**==> picture [504 x 172] intentionally omitted <==**

A simple explanation of each box before we go further with examples: 

Hotspot-in - allows to capture traffic that otherwise would be discarded by connection tracking - this way our Hotspot feature is able to provide connectivity even if networks settings are an incomplete mess ; RAW Prerouting - RAW table prerouting chain; 

- Connection tracking - packet is processed by connection tracking; Mangle Prerouting - Mangle prerouting chain; Mangle Input - Mangle input chain; Filter Input - Firewall filter input chain; HTB Global - Queue tree; 

- Simple Queues - is a feature that can be used to limit traffic for a particular target; 

- TTL - indicates an exact place where the Time To Live (TTL) of the routed packet is reduced by 1 if TTL becomes 0, a packet will be discarded; Mangle Forward - Mangle forward chain; 

- Filter Forward - Filter forward chain; 

- Accounting - Authentication, Authorization, and Accounting feature processing; RAW Output - RAW table output chain; Mangle Output - Mangle output chain; 

- Filter Output - Firewall filter output chain; 

- Routing Adjustment - this is a workaround that allows to set up policy routing in mangle chain output (routing-mark) ; Mangle Postrouting - Mangle postrouting chain; 

- Src Nat - Network Address Translation srcnat chain; 

- Dst Nat - Network Address Translation dstnat chain; 

- Hotspot-out - undo all that was done by hotspot-in for the packets that are going back to the client;
