## Basic Configuration Example 

Picture a scenario where the ether1 interface connects to your ISP, and your router needs to lease two IP addresses, each with a distinct MAC address. Traditionally, this would require the use of two physical Ethernet interfaces and an additional switch. However, a more efficient solution is to create a virtual MACVLAN interface. 

To create a MACVLAN interface, select the needed Ethernet interface. A MAC address will be automatically assigned if not manually specified: 

```
/interface macvlan
add interface=ether1 name=macvlan1
/interface macvlan print
Flags: R - RUNNING
Columns: NAME, MTU, INTERFACE, MAC-ADDRESS, MODE
#   NAME       MTU  INTERFACE  MAC-ADDRESS        MODE
0 R macvlan1  1500  ether1     76:81:BF:68:69:83  bridge
```

Now, a DHCP client can be created on ether1 and macvlan1 interfaces: 

```
/ip dhcp-client
add interface=ether1
add interface=macvlan1
```
