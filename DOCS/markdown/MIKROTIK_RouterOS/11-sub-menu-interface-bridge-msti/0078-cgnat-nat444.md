## CGNAT (NAT444) 

**==> picture [504 x 142] intentionally omitted <==**

To combat IPv4 address exhaustion, a new RFC 6598 was deployed. The idea is to use shared 100.64.0.0/10 address space inside the carrier's network and perform NAT on the carrier's edge router to a single public IP or public IP range. 

Because of the nature of such a setup, it is also called NAT444, as opposed to a NAT44 network for a 'normal' NAT environment, three different IPv4 address spaces are involved. 

CGNAT configuration on RouterOS does not differ from any other regular source NAT configuration: 

```
/ip firewall nat
```

```
 add chain=src-nat action=srcnat src-address=100.64.0.0/10 to-address=2.2.2.2 out-interface=<public_if>
```

Where: 

- 2.2.2.2 - public IP address, 

public_if - interface on provider's edge router connected to the internet 

The advantage of NAT444 is obvious, fewer public IPv4 addresses are used. But this technique comes with major drawbacks: 

The service provider router performing CGNAT needs to maintain a state table for all the address translations: this requires a lot of memory and CPU resources. 

Console gaming problems. Some games fail when two subscribers using the same outside public IPv4 address try to connect to each other. Tracking users for legal reasons means extra logging, as multiple households go behind one public address. 

649 

- Anything requiring incoming connections is broken. While this already was the case with regular NAT, end-users could usually still set up port forwarding on their NAT router. CGNAT makes this impossible. This means no web servers can be hosted here, and IP Phones cannot receive incoming calls by default either. 

- Some web servers only allow a maximum number of connections from the same public IP address, as a means to counter DoS attacks like SYN floods. Using CGNAT this limit is reached more often and some services may be of poor quality. 

- 6to4 requires globally reachable addresses and will not work in networks that employ addresses with a limited topological span. 

Packets with Shared Address Space source or destination addresses MUST NOT be forwarded across Service Provider boundaries. Service Providers MUST filter such packets on ingress links. In RouterOS this can be easily done with firewall filters on edge routers: 

```
/ip firewall filter
```

```
 add chain=input src-address=100.64.0.0/10 action=drop in-interface=<public_if>
 add chain=output dst-address=100.64.0.0/10 action=drop out-interface=<public_if>
 add chain=forward src-address=100.64.0.0/10 action=drop in-interface=<public_if>
 add chain=forward src-address=100.64.0.0/10 action=drop out-interface=<public_if>
 add chain=forward dst-address=100.64.0.0/10 action=drop out-interface=<public_if>
```

Service providers may be required to log of MAPed addresses, in a large CGN deployed network which may be a problem. Fortunately, RFC 7422 suggests a way to manage CGN translations in such a way as to significantly reduce the amount of logging required while providing traceability for abuse response. 

RFC states that instead of logging each connection, CGNs could deterministically map customer private addresses (received on the customer-facing interface of the CGN, a.k.a., internal side) to public addresses extended with port ranges. 

That means that separate NAT rules have to be added to achieve individual mappings such as the ones seen in the below example: 

Inside IP Outside IP/Port range 100.64.0.1 2.2.2.2:5000-5199 100.64.0.2 2.2.2.2:5200-5399 100.64.0.3 2.2.2.2:5400-5599 100.64.0.4 2.2.2.2:5600-5799 100.64.0.5 2.2.2.2:5800-5999 

Instead of writing the rules by hand, it is suggested to use a script instead. The following example could be adapted to any requirements of your setup. 

```
{
######## Adjustable values #########
:local StartingAddress 100.64.0.1
:local ClientCount 5
:local AddressesPerClient 2
:local PublicAddress 2.2.2.2
:local StartingPort 5000
:local PortsPerAddress 200
####################################
```
