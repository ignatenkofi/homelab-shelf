## How Fast Path Works 

FastPath is an interface driver extension, that allows a driver to talk directly to specific RouterOS facilities and skip all others. 

**==> picture [24 x 25] intentionally omitted <==**

The packet can be forwarded by a fast path handler only if at least the source interface supports a fast path. For complete fast-forwarding, destination interface support is also required. 

Currently, RouterOS has the following FastPath handlers: 

IPv4 IPv4 FastTrack Traffic Generator MPLS Bridge 

IPv4 FastPath handler is used if the following conditions are met: 

firewall rules are not configured; simple queue or queue trees with parent=global are not configured; no mesh, metarouter interface configuration; sniffer or torch is not running; connection tracking is not active; IP accounting is disabled; VRFs are not configured ( `/ip route vrf` is empty); 

690 

- A hotspot is not used ( `/ip hotspot` has no interfaces); 

IPSec policies are not configured; 

- `/tool mac-scan` is not actively used; 

- `/tool ip-scan` is not actively used. 

**==> picture [13 x 13] intentionally omitted <==**

Packets will travel the FastPath way if FastTrack is used no matter if the above conditions are met. 

Traffic Generator automatically use FastPath if the interface supports this feature. 

Currently, MPLS fast-path applies to MPLS switched traffic (frames that enter router as MPLS and must leave router as MPLS) and VPLS endpoint that do VPLS encap/decap. Other MPLS ingress and egress will operate as before. 

A Bridge handler is used if the following conditions are met: 

there are no bridge Calea, filter, NAT rules; 

- use-ip-firewall is disabled; 

- no mesh, MetaRouter interface configuration; 

- sniffer, torch, and traffic generator are not running; bridge vlan-filtering is disabled (condition is removed since RouterOS 7.2 version); bridge dhcp-snooping is disabled. 

**==> picture [13 x 13] intentionally omitted <==**

FastPath on the vlan-filtering bridge does NOT support priority-tagged packets (packets with VLAN header but VLAN ID = 0). Those packets are redirected via a slow path. 

Interfaces that support FastPath: 

**==> picture [243 x 231] intentionally omitted <==**

**----- Start of picture text -----**<br>
RouterBoard Interfaces<br>RB6xx series ether1,2<br>RB800 ether1,2<br>RB1100 series ether1-11<br>All devices Ethernet interfaces<br>wireless interfaces<br>bridge interfaces<br>VLAN, VRRP interfaces<br>bonding interfaces (RX only)<br>PPPoE, L2TP interfaces<br>EoIP, GRE, IPIP, VXLAN interfaces.<br>VPLS (starting from v7.17)<br>**----- End of picture text -----**<br>


EoIP, Gre, IPIP, VXLAN and L2TP interfaces have per-interface setting allow-fast-path. Allowing a fast path on these interfaces has a side effect of bypassing firewall, connection tracking, simple queues, queue tree with parent=global, IP accounting, IPsec, hotspot universal client, vrf assignment for encapsulated packets that go through a fast-path. Also, packet fragments cannot be received in FastPath. 

**==> picture [13 x 13] intentionally omitted <==**

Whether FastPath is being used can be verified with `/interface print stats-detail` 

691 

Only interface queue that guarantees FastPath is only-hardware-queue. If you need an interface queue other than hardware then the packet will not go fully FastPath, but there is not a big impact on performance, as "interface queue" is the last step in the packet flow. 

The packet may go Half-FastPath by switching from FastPath to SlowPath, but not the other way around. So, for example, if the receiving interface has FastPath support, but the out interface does not, then the router will process the packet by FastPath handlers as far as it can and then proceed with SlowPath. If the receiving interface does not support FastPath but the out interface does, the packet will be processed by SlowPath all the way through the router. 

**==> picture [424 x 174] intentionally omitted <==**
