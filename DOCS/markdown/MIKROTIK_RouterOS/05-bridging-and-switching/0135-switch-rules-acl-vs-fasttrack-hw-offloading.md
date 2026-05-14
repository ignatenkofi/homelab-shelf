## Switch Rules (ACL) vs. Fasttrack HW Offloading 

Some firewall rules may be implemented both via switch rules (ACL) and CPU Firewall Filter + Fasttrack HW Offloading. Both options grant near-the-wirespeed performance. So the question is which one to use? 

First, not all devices support Fasttrack HW Offloading, and without HW offloading, Firewall Filter uses only software routing, which is dramatically slower than its hardware counterpart. Second, even if Fasttrack HW Offloading is an option, a rule of thumb is: 

**==> picture [13 x 13] intentionally omitted <==**

Always use Switch Rules (ACL), if possible. 

Switch rules share the hardware memory with Fastrack connections. However, hardware resources are allocated for each Fasttrack connection while a single ACL rule can match multiple connections. For example, if you have a guest WiFi network connected to sfp-sfpplus1 VLAN 10 and you don't want it to access your internal network, simply create an ACL rule:
