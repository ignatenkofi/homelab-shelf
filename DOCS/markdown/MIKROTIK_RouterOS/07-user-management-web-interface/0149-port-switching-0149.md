## Port Switching 

To set up port switching on CRS1xx/2xx series switches, check the Bridge Hardware Offloading page. 

**==> picture [13 x 13] intentionally omitted <==**

Dynamic reserved VLAN entries (VLAN4091; VLAN4090; VLAN4089; etc.) are created in the CRS switch when switched port groups are added when a hardware offloaded bridge is created. These VLANs are necessary for internal operation and have lower precedence than userconfigured VLANs.
