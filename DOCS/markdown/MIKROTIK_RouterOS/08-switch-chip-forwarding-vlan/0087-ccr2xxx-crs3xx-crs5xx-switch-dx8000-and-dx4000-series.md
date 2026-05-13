## CCR2xxx, CRS3xx, CRS5xx: Switch DX8000 and DX4000 Series 

The devices below are based on Marvell 98DX8xxx , 98DX4xxx switch chips, or 98DX325x model. 

449 

**==> picture [516 x 386] intentionally omitted <==**

**----- Start of picture text -----**<br>
Switch  Models IPv4  IPv4  IPv6  IPv6  Nexthops IPv4 Fasttrack  IPv4 NAT  IPv4 Fasttrack/NAT,<br>Chip Routes  [1] Hosts  [7] Routes [8] Hosts [7] connections  [2,3,4] entries 2,5 VXLAN offloading<br>Per-VLAN packet/byte<br>counters<br>98DX8208 CRS309-1G-8S+IN 16K - 36K 16K 4K - 6K 8K 8K 4.5K 3.9K +<br>98DX8212 CRS312-4C+8XG-RM 16K - 36K 16K 4K - 6K 8K 8K 2.25K 2.25K +<br>98DX8216 CRS317-1G-16S+RM 120K - 240K 64K 30K - 40K 32K 8K 4.5K 4K +<br>98DX8332 CRS326- 16K - 36K 16K 4K - 6K 8K 8K 2.25K 2.25K +<br>24S+2Q+RM<br>CRS326-<br>4C+20G+2Q+RM<br>98DX3257  [6] [CRS354-48G-] 16K - 36K 16K 4K - 6K 8K 8K 2.25K 2.25K +<br>4S+2Q+RM<br>CRS354-48P-<br>4S+2Q+RM<br>98DX4310 CRS504-4XQ (IN 60K - 120K 64K 15K - 20K 32K 8K 4.5K 4K +<br>/OUT)<br>CRS510-8XS-2XQ-IN<br>RDS2216-2XG-<br>4S+4XS-2XQ<br>98DX8525 CCR2216-1G-12XS- 60K - 120K 64K 15K - 20K 32K 8K 4.5K 4K +<br>2XQ<br>CRS518-16XS-2XQ-<br>RM<br>98CX8410 CRS520-4XS-16XQ- 120K - 240K 64K 30K - 40K 32K 8K 4.5K 4K +<br>RM<br>98DX3255 [6] CCR2116-12G-4S+ 16K - 36K 16K 4K - 6K 8K 8K 2.25K 2.25K +<br>98DX8525 CCR2216-1G-12XS- 60K - 120K 64K 15K - 20K 32K 8k 4.5K 4K +<br>2XQ<br>CRS518-16XS-2XQ-<br>RM<br>**----- End of picture text -----**<br>


> 1 Depends on the complexity of the routing table. Whole-byte IP prefixes (/8, /16, /24, etc.) occupy less HW space than others (e.g., /22). Starting with Rout erOS v7.3 , when the Routing HW table gets full, only routes with longer subnet prefixes are offloaded (/30, /29, /28, etc.) while the CPU processes the shorter prefixes. In RouterOS v7.2 and before, Routing HW memory overflow led to undefined behavior. Users can fine-tune what routes to offload via routing filters (for dynamic routes) or suppressing hardware offload of static routes. IPv4 and IPv6 routing tables share the same hardware memory. 

> 2 When the HW limit of Fasttrack or NAT entries is reached, other connections will fall back to the CPU. MikroTik's smart connection offload algorithm ensures that the connections with the most traffic are offloaded to the hardware. 

> 3 Fasttrack connections share the same HW memory with ACL rules. Depending on the complexity, one ACL rule may occupy the memory of 3-6 Fasttrack connections. 

4 MPLS shares the HW memory with Fasttrack connections. Moreover, enabling MPLS requires the allocation of the entire memory region, which could otherwise store up to 768 (0.75K) Fasttrack connections. The same applies to the Bridge Port Extender. However, MPLS and BPE may use the same memory region, so enabling them both doesn't double the limitation of Fasttrack connections. 

> 5 If a Fasttrack connection requires Network Address Translation, a hardware NAT entry is created. The hardware supports both SRCNAT and DSTNAT. 

6 The switch chip has a feature set of the DX8000 series. 

> 7 DX4000/DX8000 switch chips store directly connected hosts, IPv4 /32, and IPv6 /128 route entries in the FDB table rather than the routing table. The HW memory is shared between regular FDB L2 entries (MAC), IPv4, and IPv6 addresses. The number of hosts is also limited by max-neighbor-entries in IP Settings / IPv6 Settings. 

8 IPv4 and IPv6 routing tables share the same hardware memory.
