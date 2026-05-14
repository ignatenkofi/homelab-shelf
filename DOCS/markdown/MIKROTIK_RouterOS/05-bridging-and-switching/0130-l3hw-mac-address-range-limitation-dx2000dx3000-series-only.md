## L3HW MAC Address Range Limitation (DX2000/DX3000 series only) 

Marvell Prestera DX2000 and DX3000 switch chips have a hardware limitation that allows configuring only the last (least significant) octet of the MAC address for each interface. The other five (most significant) octets are configured globally and, therefore, must be equal for all interfaces (switch ports, bridge, VLANs). In other words, the MAC addresses must be in the format " XX:XX:XX:XX:XX:?? ", where: 

441 

- " XX:XX:XX:XX:XX " part is common for all interfaces. 

- " ?? " is a variable part. 

This requirement applies only to Layer 3 (routing). Layer 2 (bridging) does not use the switch's ethernet addresses. Moreover, it does not apply to bridge ports because they use the bridge's MAC address. 

The requirement for common five octets applies to: 

Standalone switch ports (not bridge members) with hardware routing enabled ( `l3-hw-offloading=yes` ). Bridge itself. 

VLAN interfaces (those that use the bridge's MAC address by default).
