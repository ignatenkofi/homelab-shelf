## Read-only properties 

**==> picture [516 x 195] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>active  (yes | no) Whether this policy is currently in use.<br>default  (yes | no) Whether this is a default system entry.<br>dynamic  (yes | no) Whether this is a dynamically added or generated entry.<br>invalid  (yes | no) Whether this policy is invalid - the possible cause is a duplicate policy with the same src-address and dst-<br>address.<br>ph2-count  (integer) A number of active phase 2 sessions associated with the policy.<br>ph2-state  (expired | no-phase2 |  Indication of the progress of key establishing.<br>established)<br>sa-dst-address  (ip/ipv6 address; Default: ) :: SA destination IP/IPv6 address (remote peer).<br>sa-src-address  (ip/ipv6 address; Default: ) :: SA source IP/IPv6 address (local peer).<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Policy order is important starting from v6.40. Now it works similarly to firewall filters where policies are executed from top to bottom (priority parameter is removed). 

**==> picture [13 x 13] intentionally omitted <==**

All packets are IPIP encapsulated in tunnel mode, and their new IP header's src-address and dst-address are set to sa-src-address and sa-dstaddress values of this policy. If you do not use tunnel mode (id est you use transport mode), then only packets whose source and destination addresses are the same as sa-src-address and sa-dst-address can be processed by this policy. Transport mode can only work with packets that originate at and are destined for IPsec peers (hosts that established security associations). To encrypt traffic between networks (or a network and a host) you have to use tunnel mode.
