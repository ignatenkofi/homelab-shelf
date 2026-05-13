## Introduction 

Connection tracking allows the kernel to keep track of all logical network connections or sessions, and thereby relate all of the packets which may make up that connection. 

NAT relies on this information to translate all related packets in the same way. 

Because of connection tracking you can use stateful firewall functionality even with stateless protocols such as UDP. 

Firewall features affected by connection tracking: 

NAT firewall: connection-bytes connection-mark connection-type connection-state connection-limit connection-rate layer7-protocol new-connection-mark tarpit 

List of tracked connections can be seen in /ip firewall connection for IPv4 and /ipv6 firewall connection for IPv6. 

```
      [admin@3C22-atombumba] /ip firewall connection> print
      Flags: S - seen-reply, A - assured
      #    PR.. SRC-ADDRESS           DST-ADDRESS           TCP-STATE   TIMEOUT
      0    udp  10.5.8.176:5678       255.255.255.255:5678              0s
      1    udp  10.5.101.3:646        224.0.0.2:646                     5s
      2    ospf 10.5.101.161          224.0.0.5                         9m58s
      3    udp  10.5.8.140:5678       255.255.255.255:5678              8s
      4 SA tcp  10.5.101.147:48984    10.5.101.1:8291       established 4m59s
```

```
      [admin@3C22-atombumba] /ipv6 firewall connection> print
      Flags: S - seen reply, A - assured
      #    PRO.. SRC-ADDRESS                 DST-ADDRESS                 TCP-STATE
      0    udp   fe80::d6ca:6dff:fe77:3698   ff02::1
      1    udp   fe80::d6ca:6dff:fe98:7c28   ff02::1
      2    ospf  fe80::d6ca:6dff:fe73:9822   ff02::5
```
