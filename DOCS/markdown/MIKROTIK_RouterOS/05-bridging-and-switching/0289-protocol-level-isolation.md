## Protocol Level Isolation 

**==> picture [504 x 181] intentionally omitted <==**

Protocol level isolation on CRS switches can be used to enhance network security. For example, restricting DHCP traffic between the users (ether2, ether3, ether4, ether5) and allowing it only to trusted DHCP server ports (ether1) can prevent security risks like DHCP spoofing attacks. The following example shows how to configure it on CRS. 

Switch together the required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1 hw=yes
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
add bridge=bridge1 interface=ether4 hw=yes
add bridge=bridge1 interface=ether5 hw=yes
```

Set the same Community port profile for all DHCP client ports. Community port profile numbers are from 2 to 30. 

```
/interface ethernet switch port
set ether2 isolation-leakage-profile-override=2
set ether3 isolation-leakage-profile-override=2
set ether4 isolation-leakage-profile-override=2
set ether5 isolation-leakage-profile-override=2
```

And configure port isolation/leakage profile for selected Community (2) to allow DHCP traffic destined only to the port where the trusted DHCP server is located. registration status and traffic-type properties have to be set empty to apply restrictions only for DHCP protocol. 

567 

```
/interface ethernet switch port-isolation
```

```
add port-profile=2 protocol-type=dhcpv4 type=dst forwarding-type=bridged ports=ether1 registration-status=""
traffic-type=""
```
