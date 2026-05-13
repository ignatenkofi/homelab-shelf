## Change MSS 

It is a known fact that VPN links have a smaller packet size due to encapsulation overhead. A large packet with MSS that exceeds the MSS of the VPN link should be fragmented before sending it via that kind of connection. However, if the packet has a Don't Fragment flag set, it cannot be fragmented and should be discarded. On links that have broken path MTU discovery (PMTUD), it may lead to a number of problems, including problems with FTP and HTTP data transfer and e-mail services. 

In the case of a link with broken PMTUD, a decrease of the MSS of the packets coming through the VPN link resolves the problem. The following example demonstrates how to decrease the MSS value via mangle: 

```
/ip firewall mangle add out-interface=pppoe-out protocol=tcp tcp-flags=syn action=change-mss new-mss=1300
chain=forward tcp-mss=1301-65535
```

644
