## Port Level Isolation 

565 

**==> picture [504 x 224] intentionally omitted <==**

Port-level isolation is often used for Private VLAN, where: 

One or multiple uplink ports are shared among all users for accessing the gateway or router. Port group Isolated Ports is for guest users. Communication is through the uplink ports only. Port group Community 0 is for department A. Communication is allowed between the group members and through uplink ports. Port group Community X is for department X. Communication is allowed between the group members and through uplink ports. 

The Cloud Router Switches use port-level isolation profiles for Private VLAN implementation: 

Uplink ports – port-level isolation profile 0 Isolated ports – port-level isolation profile 1 Community 0 ports - port-level isolation profile 2 Community X (X <= 30) ports - port-level isolation profile X 

This example requires a group of switched ports. Assume that all ports used in this example are in one switch group. 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
add bridge=bridge1 interface=ether9 hw=yes
add bridge=bridge1 interface=ether10 hw=yes
```

The first part of port isolation configuration is setting the Uplink port – set a port profile to 0 for ether2: 

```
/interface ethernet switch port
set ether2 isolation-leakage-profile-override=0
```

Then continue with setting isolation profile 1 to all isolated ports and adding the communication port for port isolation profile 1: 

```
/interface ethernet switch port
set ether5 isolation-leakage-profile-override=1
set ether6 isolation-leakage-profile-override=1
```

```
/interface ethernet switch port-isolation
add port-profile=1 ports=ether2 type=dst
```

Configuration to set Community 2 and Community 3 ports is similar: 

566 

```
/interface ethernet switch port
set ether7 isolation-leakage-profile-override=2
set ether8 isolation-leakage-profile-override=2
```

```
/interface ethernet switch port-isolation
add port-profile=2 ports=ether2,ether7,ether8 type=dst
```

```
/interface ethernet switch port
set ether9 isolation-leakage-profile-override=3
set ether10 isolation-leakage-profile-override=3
```

```
/interface ethernet switch port-isolation
add port-profile=3 ports=ether2,ether9,ether10 type=dst
```
