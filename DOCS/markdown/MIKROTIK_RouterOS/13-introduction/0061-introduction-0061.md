## Introduction 

MLAG (Multi-chassis Link Aggregation Group) implementation in RouterOS allows configuring LACP bonds on two separate devices, while the client device believes to be connected to the same machine. This provides a physical redundancy in case of switch failure. All CRS3xx, CRS5xx series switches, and CCR2116, CCR2216 devices can be configured with MLAG using RouterOS version 7. 

Both peers establish the MLAG interfaces and update the bridge host table over `peer-port` using ICCP (Inter Chassis Control Protocol). RouterOS ICCP does not require an IP configuration, it sends untagged Layer2 packets marked with EtherType 0x88B5 and a destination MAC address of 01:80:C2:00:00: 0E. ICCP packets are link-local, meaning they are always received and handled by the MLAG devices themselves and never forwarded to other parts of the network. The peer-ports on each MLAG device must be directly connected to each other. It is also recommended to keep the untagged VLAN used by the peer ports separate from the rest of your network, either by assigning a dedicated untagged VLAN (using `pvid` ), or by setting the peer port to only allow VLAN tagged frames (using `frame-types=admit-only-vlan-tagged` ). Peer ports can be configured as single Ethernet interfaces or bonding interfaces. However, using a bonding interface is recommended, as it helps prevent a single interface failure from affecting connectivity, especially when both MLAG nodes are still up and running. 

When `peer-port` is running and ICCP is established, the primary device election happens and `system-id` will be selected. The peer with the lowest `pri ority` will act as the primary device. If the priorities are the same, the peer with the lowest bridge MAC address will become the primary. This `system-id` is used for STP BPDU bridge identifier and LACP system ID. The MLAG supports STP, RSTP or MSTP protocols. Use the same STP priority and the same STP configuration on dual-connected bridge ports on both nodes. When MLAG bridges are elected as STP root, then both devices will show as root bridges under the bridge monitor. 

**==> picture [13 x 13] intentionally omitted <==**

The MLAG is not compatible with L3 hardware offloading. When using MLAG, the L3 hardware offloading must be disabled. 

The MLAG is not compatible with Multiple VLAN Registration protocol (MVRP). Registered VLANs on dual-connected bonds does not get synchronized to other MLAG node. 

776 

**==> picture [504 x 389] intentionally omitted <==**
