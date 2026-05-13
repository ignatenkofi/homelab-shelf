## Summary 

RoMON stands for "Router Management Overlay Network". RoMON works by establishing an independent MAC layer peer discovery and data forwarding network. RoMON packets are encapsulated with EtherType 0x88bf and DST-MAC 01:80:c2:00:88:bf and its network operate independently of L2 or L3 forwarding configuration. When RoMON is enabled, any received RoMON packets will not be displayed by sniffer or torch tools. 

Each router on the RoMON network is assigned its RoMON ID. RoMON ID can be selected from the port MAC address or specified by the user. 

RoMON protocol does not provide encryption services. Encryption is provided at the "application" level, by e.g. using ssh or by using a secure WinBox. 

**==> picture [13 x 13] intentionally omitted <==**

RoMON packets can be forwarded through network switches or bridges, unless there are specific restrictions on multicast traffic. When using a MikroTik bridge with hardware offloading, these packets are treated like regular multicast packets and are flooded across the network. 

Since RouterOS v7.17, if the RoMON service is enabled and the switch chip supports ACL rules, dynamic rules are automatically created to redirect these packets to the CPU, where the RoMON service operates. However, if the switch does not support ACL rules and configuration does not align, such as when CPU and RoMON untagged packets are not in the same VLAN, the RoMON service might not function as expected.
