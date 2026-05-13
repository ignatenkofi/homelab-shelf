## Traffic Storm Control 

The same Ingress Port policer also can be used for traffic storm control to prevent disruptions on Layer 2 ports caused by broadcast, multicast, or unicast traffic storms. 

Broadcast storm control example on ether5 port with 500 packet limit per second: 

```
/interface ethernet switch ingress-port-policer
```

```
add port=ether5 rate=500 meter-unit=packet packet-types=broadcast
```

Example with multiple packet types which includes ARP and ND protocols and unregistered multicast traffic. Unregistered multicast is traffic that is not defined in the Multicast Forwarding Database. 

```
/interface ethernet switch ingress-port-policer
```

```
add port=ether5 rate=5k meter-unit=packet packet-types=broadcast,arp-or-nd,unregistered-multicast
```

571
