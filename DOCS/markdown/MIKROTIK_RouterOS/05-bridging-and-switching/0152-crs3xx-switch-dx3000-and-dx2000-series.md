## CRS3xx: Switch DX3000 and DX2000 Series 

The devices below are based on Marvell 98DX224S, 98DX226S , 98DX2528, or 98DX3236 switch chip models. 

**==> picture [516 x 348] intentionally omitted <==**

**----- Start of picture text -----**<br>
The  98DX3255  and  98DX3257  models are exceptions, which have a feature set of the DX8000 rather than the DX3000 series.<br>Below are some important features that these devices are missing when compared to other switch models:<br>Fasttrack and NAT connection offloading;<br>per-VLAN packet and byte counters;<br>VXLAN offloading.<br>Switch Chip Models IPv4 Route Prefixes [1] IPv6 Route Prefixes [2] Nexthops ECMP paths per prefix [3]<br>98DX3236 CRS305-1G-4S+IN 13312 3328 4K 8<br>CRS326-24G-2S+ (RM/IN)<br>CRS328-24P-4S+RM<br>CRS328-4C-20S-4S+RM<br>98DX226S CRS305-1G-4S+OUT (FiberBox Plus) 13312 3328 4K 8<br>CRS310-1G-5S-4S+ (netFiber 9/IN)<br>CRS310-8G+2S+IN<br>CRS318-16P-2S+OUT (netPower 16P)<br>CRS320-8P-8B-4S+RM<br>CRS418-8P-8G-2S+RM<br>98DX224S CRS318-1Fi-15Fr-2S-OUT (netPower 15FR) 13312  3328 4K 8<br>98DX2528 CRS304-4XG-IN 13312 3328 4K 8<br>**----- End of picture text -----**<br>

1 Since the total amount of routes that can be offloaded is limited, prefixes with higher netmask are preferred to be forwarded by hardware (e.g., /32, /30, /29, etc.), any other prefixes that do not fit in the HW table will be processed by the CPU. Directly connected hosts are offloaded as /32 (IPv4) or /128 (IPv6) route prefixes. The number of hosts is also limited by max-neighbor-entries in IP Settings / IPv6 Settings. 

> 2 IPv4 and IPv6 routing tables share the same hardware memory. 

3 If a route has more paths than the hardware ECMP limit (X), only the first X paths get offloaded.
