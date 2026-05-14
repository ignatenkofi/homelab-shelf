## "Loopback" IP address 

Although not a strict requirement, it is advisable to configure routers participating in the MPLS network with "loopback" IP addresses (not attached to any real network interface) to be used by LDP to establish sessions. 

This serves 2 purposes: 

- as there is only one LDP session between any 2 routers, no matter how many links connect them, the loopback IP address ensures that the LDP session is not affected by interface state or address changes 

- use of loopback address as LDP transport address ensures proper penultimate hop popping behavior when multiple labels are attached to the packet as in the case of VPLS 

In RouterOS "loopback" IP address can be configured by creating a dummy bridge interface without any ports and adding the address to it. For example: 

```
/interface bridge add name=lo
```

```
/ip address add address=255.255.255.1/32 interface=lo
```

IP connectivity 

842 

As LDP distributes labels for active routes, the essential requirement is properly configured IP routing. LDP by default distributes labels for active IGP routes (that is - connected, static, and routing protocol learned routes, except BGP). 

For instructions on how to set up properly IGP refer to appropriate documentation sections: 

OSPF Static Routing etc 

LDP supports ECMP routes. 

You should be able to reach any loopback address from any location of your network before continuing with the LDP configuration. Connectivity can be verified with the ping tool running from loopback address to loopback address.
