## Create a routable VLAN interface on SwitchA , SwitchB, and SwitchC : 

```
/interface vlan
```

```
add interface=bridge name=MGMT vlan-id=99
```

The Router needs a routable VLAN interface to be created on the bonding interface, use these commands to create a VLAN interface on the Router : 

```
/interface vlan
add interface=bond_1-2-3-4 name=MGMT vlan-id=99
```

For this guide, we are going to use these addresses for each device: 

Device Address Router 192.168.99.1 SwitchA 192.168.99.2 

575 

SwitchB 192.168.99.3 SwitchC 192.168.99.4 

Add an IP address for each switch device on the VLAN interface (change X to the appropriate number): 

```
/ip address
add address=192.168.99.X/24 interface=MGMT
```

Do not forget to add the default gateway and specify a DNS server on the switch devices: 

```
/ip route
add gateway=192.168.99.1
/ip dns
set servers=192.168.99.1
```
