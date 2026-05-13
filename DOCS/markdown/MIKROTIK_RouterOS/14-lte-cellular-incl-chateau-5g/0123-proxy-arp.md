## Proxy ARP 

A router with a properly configured proxy ARP feature acts as a transparent ARP proxy between different networks. 

This behavior can be useful, for example, if you want to assign dial-in (ppp, pppoe, pptp) clients' IP addresses from the same address space as used on the connected LAN. 

Proxy ARP can be enabled on each interface individually with the command `arp=proxy-arp` : 

Setup proxy ARP: 

866 

```
 [admin@MikroTik] /interface ethernet> set 1 arp=proxy-arp
```

```
 [admin@MikroTik] /interface ethernet> print
```

```
 Flags: X - disabled, R - running
   #    NAME                 MTU   MAC-ADDRESS         ARP
   0  R ether1              1500  00:30:4F:0B:7B:C1 enabled
   1  R ether2              1500  00:30:4F:06:62:12 proxy-arp
```
