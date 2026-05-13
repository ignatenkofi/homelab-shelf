## Standards: `IEEE 802.1Q, IEEE 802.1ad` 

Virtual Local Area Network (VLAN) is a Layer 2 method that allows multiple Virtual LANs on a single physical interface (ethernet, wireless, etc.), giving the ability to segregate LANs efficiently. 

You can use MikroTik RouterOS (as well as Cisco IOS, Linux, and other router systems) to mark these packets as well as to accept and route marked ones. 

As VLAN works on OSI Layer 2, it can be used just like any other network interface without any restrictions. VLAN successfully passes through regular Ethernet bridges. 

You can also transport VLANs over wireless links and put multiple VLAN interfaces on a single wireless interface. Note that as VLAN is not a full tunnel protocol (i.e., it does not have additional fields to transport MAC addresses of sender and recipient), the same limitation applies to bridging over VLAN as to bridging plain wireless interfaces. In other words, while wireless clients may participate in VLANs put on wireless interfaces, it is not possible to have VLAN put on a wireless interface in station mode bridged with any other interface.
