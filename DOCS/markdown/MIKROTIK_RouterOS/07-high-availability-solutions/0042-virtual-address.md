## Virtual Address 

784 

**==> picture [504 x 349] intentionally omitted <==**

Virtual IP associated with VR must be identical and set on all VR nodes. All virtual and real addresses should be from the same network. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS can not be configured as Owner. VRRP address and real IP address should not be the same. 

If the Master of VR is associated with multiple IP addresses, then Backup routers belonging to the same VR must also be associated with the same set of virtual IP addresses. If the virtual address on the Master is not also on Backup a misconfiguration exists and VRRP advertisement packets will be discarded. 

All Virtual Router members can be configured so that virtual IP is not the same as physical IP. Such a virtual address can be called a floating or pure virtual IP address. The advantage of this setup is the flexibility given to the administrator. Since the virtual IP address is not the real address of any one of the participant routers, the administrator can change these physical routers or their addresses without any need to reconfigure the virtual router itself. 

In IPv6 networks, the first address is always a link-local address associated with VR. If multiple IPv6 addresses are configured, then they are added to the advertisement packet after the link-local address.
