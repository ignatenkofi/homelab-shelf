## `/ip firewall nat` 

```
add action=masquerade chain=srcnat dst-address=10.0.0.3 out-interface=LAN protocol=tcp src-address=10.0.0.0/24
```

After configuring the rule above: 

1.  the client sends a packet with a source IP address of 10.0.0.2 to a destination IP address of 172.16.16.1 on port 443 to request some web resources; 

2.  the router destination NATs the packet to 10.0.0.3 and replaces the destination IP address in the packet accordingly. It also source NATs the packet and replaces the source IP address in the packet with the IP address on its LAN interface. The destination IP address is 10.0.0.3, and the source IP address is 10.0.0.1; 

3.  the web server replies to the request and sends the reply with a source IP address of 10.0.0.3 back to the router's LAN interface IP address of 10.0.0.1; 

4.  the router determines that the packet is part of a previous connection and undoes both the source and destination NAT, and puts the original destination IP address of 10.0.0.3 into the source IP address field, and the original source IP address of 172.16.16.1 into the destination IP address field
