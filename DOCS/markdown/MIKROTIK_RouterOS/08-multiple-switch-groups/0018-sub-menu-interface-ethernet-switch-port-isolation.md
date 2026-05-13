## Sub-menu: `/interface ethernet switch port-isolation` 

Sub-menu: `/interface ethernet switch port-leakage` 

**==> picture [507 x 109] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Enables or disables port isolation/leakage entry.<br>flow-id  (0..63; Default: none )<br>forwarding-type  (bridged; routed; Default: bridged,routed ) Matching traffic forwarding type on Cloud Router Switch.<br>mac-profile  (community1 | community2 | isolated | promiscuous;  Matching MAC isolation/leakage profile.<br>Default: none )<br>**----- End of picture text -----**<br>


425 

**==> picture [507 x 213] intentionally omitted <==**

**----- Start of picture text -----**<br>
port-profile  (0..31; Default: none ) Matching Port isolation/leakage profile.<br>ports  (ports; Default: none ) Isolated/leaked ports.<br>protocol-type  (arp; nd; dhcpv4; dhcpv6; ripv1; Default: arp,nd, Included protocols for isolation/leakage.<br>dhcpv4,dhcpv6,ripv1 )<br>registration-status  (known; unknown; Default: known,unknown ) Registration status for matching packets. Known are present in UFDB and<br>MFDB, and unknown are not.<br>traffic-type  (unicast; multicast; broadcast; Default: unicast, Matching traffic type.<br>multicast,broadcast )<br>type  (dst | src; Default: src ) Lookup type of the isolation/leakage entry:<br>src - Entry applies to ingress packets of the ports.<br>dst - Entry applies to egress packets of the ports.<br>vlan-profile  (community1 | community2 | isolated | promiscuous;  Matching VLAN isolation/leakage profile.<br>Default: none )<br>**----- End of picture text -----**<br>
