## DHCP Snooping and DHCP Option 82 

DHCP Snooping and DHCP Option 82 is supported by bridge. The DHCP Snooping is a Layer2 security feature, that limits unauthorized DHCP servers from providing malicious information to users. In RouterOS, you can specify which bridge ports are trusted (where known DHCP server resides and DHCP messages should be forwarded) and which are untrusted (usually used for access ports, received DHCP server messages will be dropped). The DHCP Option 82 is additional information (Agent Circuit ID and Agent Remote ID) provided by DHCP Snooping enabled devices that allow identifying the device itself and DHCP clients. 

**==> picture [504 x 237] intentionally omitted <==**

386 

In this example, SW1 and SW2 are DHCP Snooping, and Option 82 enabled devices. First, we need to create a bridge, assign interfaces and mark trusted ports. Use these commands on SW1 : 

```
/interface bridge
add name=bridge
/interface bridge port
add bridge=bridge interface=ether1
add bridge=bridge interface=ether2 trusted=yes
```

For SW2, the configuration will be similar, but we also need to mark ether1 as trusted, because this interface is going to receive DHCP messages with Option 82 already added. You need to mark all ports as trusted if they are going to receive DHCP messages with added Option 82, otherwise these messages will be dropped. Also, we add ether3 to the same bridge and leave this port untrusted, imagine there is an unauthorized (rogue) DHCP server. Use these commands on SW2 : 

```
/interface bridge
add name=bridge
/interface bridge port
add bridge=bridge interface=ether1 trusted=yes
add bridge=bridge interface=ether2 trusted=yes
add bridge=bridge interface=ether3
```

Then we need to enable DHCP Snooping and Option 82. In case your DHCP server does not support DHCP Option 82 or you do not implement any Option 82 related policies, this option can be disabled. Use these commands on SW1 and SW2 : 

```
/interface bridge
```

```
set [find where name="bridge"] dhcp-snooping=yes add-dhcp-option82=yes
```

Now both devices will analyze what DHCP messages are received on bridge ports. The SW1 is responsible for adding and removing the DHCP Option 82. The SW2 will limit rogue DHCP server from receiving any discovery messages and drop malicious DHCP server messages from ether3. 

**==> picture [13 x 13] intentionally omitted <==**

Currently, CRS3xx, CRS5xx series switches, CCR2116, CR2216 routers, and 88E6393X, 88E6191X, 88E6190 switch chips fully support hardware offloaded DHCP Snooping and Option 82. For CRS1xx and CRS2xx series switches it is possible to use DHCP Snooping along with VLAN switching, but then you need to make sure that DHCP packets are sent out with the correct VLAN tag using egress ACL rules. Other devices are capable of using DHCP Snooping and Option 82 features along with hardware offloading, but you must make sure that there is no VLAN-related configuration applied on the device, otherwise, DHCP Snooping and Option 82 might not work properly. See the Br idge Hardware Offloading section with supported features. 

**==> picture [13 x 13] intentionally omitted <==**

Starting from RouterOS v7.17, DHCP snooping is supported with hardware offloading bonding interfaces.
