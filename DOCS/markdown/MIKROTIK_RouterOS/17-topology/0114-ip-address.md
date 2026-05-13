## `/ip address` 

```
add address=192.168.10.10/24 interface=ether1 network=192.168.10.0
```

Then configure Group Management Protocol on the same interface: 

```
/routing gmp
add groups=229.1.1.1 interfaces=ether1
```

It is now possible to check your multicast network to see if routers or switches have created the appropriate multicast forwarding entries and whether multicast data is being received on the interface (see the interface stats, or use a Packet Sniffer and Torch). 

1085
