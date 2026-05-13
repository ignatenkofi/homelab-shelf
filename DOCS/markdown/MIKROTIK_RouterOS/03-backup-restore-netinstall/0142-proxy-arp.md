## Proxy ARP 

A router with properly configured proxy ARP feature acts as a transparent ARP proxy between directly connected networks. This behavior can be useful, for example, if you want to assign dial-in (PPP, PPPoE, PPTP) clients IP addresses from the same address space as used on the connected LAN. 

155 

**==> picture [504 x 324] intentionally omitted <==**

Let's look at the example setup from the image above. Host A (172.16.1.2) on Subnet A wants to send packets to Host D (172.16.2.3) on Subnet B. Host A has a /16 subnet mask which means that Host A believes that it is directly connected to all 172.16.0.0/16 network (the same LAN). Since the Host A believes that is directly connected it sends an ARP request to the destination to clarify the MAC address of Host D. (in the case when Host A finds that destination IP address is not from the same subnet it sends a packet to the default gateway.). Host A broadcasts an ARP request on Subnet A. 

Info from packet analyzer software: 

```
 No.     Time   Source             Destination       Protocol  Info
 12   5.133205  00:1b:38:24:fc:13  ff:ff:ff:ff:ff:ff  ARP      Who has 173.16.2.3?  Tell 173.16.1.2
```

```
Packet details:
```

```
Ethernet II, Src: (00:1b:38:24:fc:13), Dst: (ff:ff:ff:ff:ff:ff)
    Destination: Broadcast (ff:ff:ff:ff:ff:ff)
    Source: (00:1b:38:24:fc:13)
    Type: ARP (0x0806)
Address Resolution Protocol (request)
    Hardware type: Ethernet (0x0001)
    Protocol type: IP (0x0800)
    Hardware size: 6
    Protocol size: 4
    Opcode: request (0x0001)
    [Is gratuitous: False]
    Sender MAC address: 00:1b:38:24:fc:13
    Sender IP address: 173.16.1.2
    Target MAC address: 00:00:00:00:00:00
    Target IP address: 173.16.2.3
```

156 

With this ARP request, Host A (172.16.1.2) is asking Host D (172.16.2.3) to send its MAC address. The ARP request packet is then encapsulated in an Ethernet frame with the MAC address of Host A as the source address and a broadcast (FF:FF:FF:FF:FF:FF) as the destination address. Layer 2 broadcast means that frame will be sent to all hosts in the same layer 2 broadcast domain which includes the ether0 interface of the router, but does not reach Host D, because router by default does not forward layer 2 broadcasts. 

Since the router knows that the target address (172.16.2.3) is on another subnet but it can reach Host D, it replies with its own MAC address to Host A. 

```
No.     Time   Source            Destination         Protocol   Info
13   5.133378  00:0c:42:52:2e:cf  00:1b:38:24:fc:13   ARP        172.16.2.3 is at 00:0c:42:52:2e:cf
Packet details:
Ethernet II, Src: 00:0c:42:52:2e:cf, Dst: 00:1b:38:24:fc:13
   Destination: 00:1b:38:24:fc:13
   Source: 00:0c:42:52:2e:cf
   Type: ARP (0x0806)
Address Resolution Protocol (reply)
   Hardware type: Ethernet (0x0001)
   Protocol type: IP (0x0800)
   Hardware size: 6
   Protocol size: 4
   Opcode: reply (0x0002)
   [Is gratuitous: False]
   Sender MAC address: 00:0c:42:52:2e:cf
   Sender IP address: 172.16.1.254
   Target MAC address: 00:1b:38:24:fc:13
   Target IP address: 172.16.1.2
```

This is the Proxy ARP reply that the router sends to Host A. Router sends back unicast proxy ARP reply with its own MAC address as the source address and the MAC address of Host A as the destination address, by saying "send these packets to me, and I'll get it to where it needs to go." 

When Host A receives ARP response it updates its ARP table, as shown: 

```
C:\Users\And>arp -a
Interface: 173.16.2.1 --- 0x8
  Internet Address      Physical Address      Type
  173.16.1.254          00-0c-42-52-2e-cf    dynamic
  173.16.2.3            00-0c-42-52-2e-cf    dynamic
  173.16.2.2            00-0c-42-52-2e-cf    dynamic
```

After MAC table update, Host A forwards all the packets intended for Host D (172.16.2.3) directly to router interface ether0 (00:0c:42:52:2e:cf) and the router forwards packets to Host D. The ARP cache on the hosts in Subnet A is populated with the MAC address of the router for all the hosts on Subnet B. Hence, all packets destined to Subnet B are sent to the router. The router forwards those packets to the hosts in Subnet B. 

Multiple IP addresses by the host are mapped to a single MAC address (the MAC address of this router) when proxy ARP is used. 

Proxy ARP can be enabled on each interface individually with command arp=proxy-arp: 

```
 [admin@MikroTik] /interface ethernet> set 1 arp=proxy-arp
 [admin@MikroTik] /interface ethernet> print
 Flags: X - disabled, R - running
   #    NAME                 MTU   MAC-ADDRESS         ARP
   0  R ether1              1500  00:30:4F:0B:7B:C1 enabled
   1  R ether2              1500  00:30:4F:06:62:12 proxy-arp
 [admin@MikroTik] interface ethernet>
```

Local Proxy ARP 

157 

if the arp property is set to local-proxy-arp on an interface, then the router performs proxy ARP to/from this interface only. I.e. for traffic that comes in and goes out of the same interface. In a normal LAN, the default behavior is for two network hosts to communicate directly with each other, without involving the router. 

This is done to support (Ethernet) switch features, like RFC 3069, where the individual ports are NOT allowed to communicate with each other, but they are allowed to talk to the upstream router. As described in RFC 3069, it is possible to allow these hosts to communicate through the upstream router by proxy_arp'ing. Don't need to be used together with proxy_arp. This technology is known by different names: 

- In RFC 3069 it is called VLAN Aggregation; 

- Cisco and Allied Telesis call it Private VLAN; Hewlett-Packard calls it Source-Port filtering or port-isolation; Ericsson calls it MAC-Forced Forwarding (RFC Draft).
