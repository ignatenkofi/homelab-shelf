## Bridge VLAN Filtering 

Bridge VLAN Filtering provides VLAN-aware Layer 2 forwarding and VLAN tag modifications within the bridge. This set of features makes bridge operation more similar to a traditional Ethernet switch and allows overcoming Spanning Tree compatibility issues compared to the configuration when VLAN interfaces are bridged. Bridge VLAN Filtering configuration is highly recommended to comply with STP (IEEE 802.1D), RSTP (IEEE 802.1W) standards and is mandatory to enable MSTP (IEEE 802.1s) support in RouterOS. 

The main VLAN setting is `vlan-filtering` which globally controls VLAN-awareness and VLAN tag processing in the bridge. If `vlanfiltering=no` is configured, the bridge ignores VLAN tags, works in a shared-VLAN-learning (SVL) mode, and cannot modify VLAN tags of packets. Turning on `vlan-filtering` enables all bridge VLAN related functionality and independent-VLAN-learning (IVL) mode. Besides joining the ports for Layer2 forwarding, the bridge itself is also an interface therefore it has Port VLAN ID (pvid). 

**==> picture [13 x 13] intentionally omitted <==**

Currently, CRS3xx, CRS5xx series switches, CCR2116, CCR2216 routers and RTL8367, 88E6393X, 88E6191X, 88E6190, MT7621, MT7531, EN7523 switch chips (since RouterOS v7) are capable of using bridge VLAN filtering and hardware offloading at the same time, other devices will not be able to use the benefits of a built-in switch chip when bridge VLAN filtering is enabled. Other devices should be configured according to the method described in the Basic VLAN switching guide. If an improper configuration method is used, your device can cause throughput issues in your network.
