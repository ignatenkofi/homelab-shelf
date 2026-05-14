## Bridge Hardware Offloading 

It is possible to switch multiple ports together if a device has a built-in switch chip. While a bridge is a software feature that will consume CPU's resources, the bridge hardware offloading feature will allow you to use the built-in switch chip to forward packets. This allows you to achieve higher throughput if configured correctly. 

In previous versions (prior to RouterOS v6.41) you had to use the master-port property to switch multiple ports together, but in RouterOS v6.41 this property is replaced with the bridge hardware offloading feature, which allows your to switch ports and use some of the bridge features, for example, S panning Tree Protocol. 

**==> picture [13 x 13] intentionally omitted <==**

- When upgrading from previous versions (before RouterOS v6.41), the old master-port configuration is automatically converted to the new Br idge Hardware Offloading configuration. When downgrading from newer versions (RouterOS v6.41 and newer) to older versions (before RouterOS v6.41) the configuration is not converted back, a bridge without hardware offloading will exist instead, in such a case you need to reconfigure your device to use the old master-port configuration. 

Below is a list of devices and feature that supports hardware offloading (+) or disables hardware offloading (-): 

**==> picture [502 x 221] intentionally omitted <==**

**----- Start of picture text -----**<br>
RouterBoard/[Switch Chip] Model Features in Switch  Bridge STP Bridge  Bridge IGMP  Bridge DHCP  Bridge VLAN  Bonding  [1,] Horizon<br>menu /RSTP MSTP Snooping Snooping Filtering 2 1<br>CRS3xx, CRS5xx series, CCR2116,  + + + + + + +  [3] -<br>CCR2216<br>[88E6393X, 88E6191X, 88E6190] + + + +  [5] +  [5] +  [6] +  [4] -<br>[MT7621, MT7531, EN7523] + +  [6] +  [6] - - +  [6] - -<br>[RTL8367] + +  [6] +  [6] - - +  [6] - -<br>CRS1xx/CRS2xx series + + - + [7] +  [8] - - -<br>[QCA8337] + + - - +  [7] - - -<br>[Atheros8327] + + - - +  [7] - - -<br>[Atheros8316] + + - - +  [7] - - -<br>[Atheros8227] + + - - - - - -<br>[Atheros7240] + + - - - - - -<br>[IPQ-PPE] +  [9] - - - - - - -<br>[ICPlus175D] + - - - - - - -<br>**----- End of picture text -----**<br>

Footnotes: 

1.  The HW offloading will be disabled only for the specific bridge port, not the entire bridge. 

370 

2.  Only `802.3ad` (LACP), `balance-xor` (static LAG) and `active-backup` bonding modes are hardware offloaded. Other bonding modes do not support HW offloading. 

3.  The CRS3xx, CRS5xx series switches, CCR2116, CCR2216 routers will always use Layer2+Layer3+Layer4 for a transmit hash policy. Changing the transmit hash policy manually while HW offloading is used will have no effect. 

4.  The 88E6393X, 88E6191X, 88E6190 switch chips are limited to Layer2 transmit hash. Changing the transmit hash policy manually while HW offloading is used will have no effect. 

5.  The 88E6393X, 88E6191X, 88E6190 switch chips do not support QinQ configurations. They are limited to parsing only the first VLAN tag, any feature that require reading data after the VLAN tag, such as `dhcp-snooping` or `igmp-snooping` , will not function properly in QinQ setups. As a result, double-tagged DHCP or IGMP packets may be forwarded to incorrect switch ports and may lead to inaccurate MDB entries, causing multicast traffic to be flooded incorrectly. 

6.  The HW vlan-filtering and R/M/STP was added in the RouterOS 7.1 for RTL8367, MT7621, MT7531, EN7523. The switch does not support other ether-type 0x88a8 or 0x9100 (only 0x8100 is supported) and no tag-stacking. Using these features will disable HW offload. 

7.  The feature will not work properly in VLAN switching setups. 

8.  The feature will not work properly in VLAN switching setups. It is possible to correctly snoop DHCP packets only for a single VLAN, but this requires that these DHCP messages get tagged with the correct VLAN tag using an ACL rule, for example, `/interface ethernet switch acl add dst-l3-port=67-68 ip-protocol=udp mac-protocol=ip new-customer-vid=10 src-ports=switch1cpu` . DHCP Option 82 will not contain any information regarding VLAN-ID. 

9.  Currently, HW offloaded bridge support for the IPQ-PPE switch chip is still a work in progress. We recommend using, the default, non-HW offloaded bridge (enabled RSTP). 

**==> picture [13 x 13] intentionally omitted <==**

When upgrading from older versions (before RouterOS v6.41), only the master-port configuration is converted. For each master-port a bridge will be created. VLAN configuration is not converted and should not be changed, check the Basic VLAN switching guide to be sure how VLAN switching should be configured for your device. 

Bridge Hardware Offloading should be considered as port switching, but with more possible features. By enabling hardware offloading you are allowing a built-in switch chip to process packets using its switching logic. The diagram below illustrates that switching occurs before any software related action. 

**==> picture [504 x 230] intentionally omitted <==**

A packet that is received by one of the ports always passes through the switch logic first. Switch logic decides which ports the packet should be going to (most commonly this decision is made based on the destination MAC address of a packet, but there might be other criteria that might be involved based on the packet and the configuration). In most cases the packet will not be visible to RouterOS (only statistics will show that a packet has passed through), this is because the packet was already processed by the switch chip and never reached the CPU. 

Though it is possible in certain situations to allow a packet to be processed by the CPU, this is usually called a packet forwarding to the switch CPU port (or the bridge interface in bridge VLAN filtering scenario). This allows the CPU to process the packet and lets the CPU to forward the packet. Passing the packet to the CPU port will give you the opportunity to route packets to different networks, perform traffic control and other software related packet processing actions. To allow a packet to be processed by the CPU, you need to make certain configuration changes depending on your needs and on the device you are using (most commonly passing packets to the CPU are required for VLAN filtering setups). Check the manual page for your specific device: 

CRS1xx/2xx series switches 

CRS3xx, CRS5xx series switches and CCR2116, CCR2216 routers 

371 

non-CRS series switches 

**==> picture [13 x 13] intentionally omitted <==**

Certain bridge and Ethernet port properties are directly related to switch chip settings. Changing such properties can trigger a switch chip reset , temporarily disabling all Ethernet ports that are on the switch chip for the settings to take effect. This must be taken into account whenever changing properties in production environments. Such properties include DHCP Snooping, IGMP Snooping, VLAN filtering, L2MTU, Flow Control, and others. The exact settings that can trigger a switch chip reset depend on the device's model. 

**==> picture [13 x 13] intentionally omitted <==**

The CRS1xx/2xx series switches support multiple hardware offloaded bridges per switch chip. All other devices support only one hardware offloaded bridge per switch chip. Use the hw=yes/no parameter to select which bridge will use hardware offloading.
