## VLAN Tunneling (Q-in-Q) 

Since RouterOS v6.43 it is possible to use a provider bridge (IEEE 802.1ad) and Tag Stacking VLAN filtering, and hardware offloading at the same time. The configuration is described in the Bridge VLAN Tunneling (Q-in-Q) section. 

**==> picture [13 x 13] intentionally omitted <==**

Devices with switch chip Marvell-98DX3257 (e.g. CRS354 series) do not support VLAN filtering on 1Gbps Ethernet interfaces for other VLAN types ( `0x88a8` and `0x9100` ).
