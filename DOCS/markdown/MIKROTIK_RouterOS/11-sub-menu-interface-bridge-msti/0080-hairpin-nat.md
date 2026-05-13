## Hairpin NAT 

Hairpin network address translation (NAT Loopback) is where the device on the LAN can access another machine on the LAN via the public IP address of the gateway router. 

**==> picture [505 x 196] intentionally omitted <==**

In the above example, the gateway router has the following `dst-nat` configuration rule: 

```
/ip firewall nat add chain=dstnat action=dst-nat dst-address=172.16.16.1 dst-port=443 to-addresses=10.0.0.3 to-
ports=443 protocol=tcp
```

When a user from the PC at home establishes a connection to the web server, the router performs DST NAT as configured: 

1.  the client sends a packet with a source IP address of 192.168.88.1 to a destination IP address of 172.16.16.1 on port 443 to request some web resources; 

2.  the router destination NAT`s the packet to 10.0.0.3 and replaces the destination IP address in the packet accordingly. The source IP address stays the same: 192.168.88.1; 

3.  the server replies to the client's request and the reply packet has a source IP address of 10.0.0.3 and a destination IP address of 192.168.88.1. 

4.  the router determines that the packet is part of a previous connection and undoes the destination NAT, and puts the original destination IP address into the source IP address field. The destination IP address is 192.168.88.1, and the source IP address is 172.16.16.1; 

5.  The client receives the reply packet it expects, and the connection is established; 

**==> picture [505 x 139] intentionally omitted <==**

652 

**==> picture [505 x 57] intentionally omitted <==**

- But, there will be a problem , when a client on the same network as the web server requests a connection to the web server's public IP address: 

   1.  the client sends a packet with a source IP address of 10.0.0.2 to a destination IP address of 172.16.16.1 on port 443 to request some web resources; 

   2.  the router destination NATs the packet to 10.0.0.3 and replaces the destination IP address in the packet accordingly. The source IP address stays the same: 10.0.0.2; 

   3.  the server replies to the client's request. However, the source IP address of the request is on the same subnet as the web server. The web server does not send the reply back to the router but sends it back directly to 10.0.0.2 with a source IP address in the reply of 10.0.0.3; 

   4.  The client receives the reply packet, but it discards it because it expects a packet back from 172.16.16.1, and not from 10.0.0.3; 

To resolve this issue, we will configure a new src-nat rule (the hairpin NAT rule) as follows:
