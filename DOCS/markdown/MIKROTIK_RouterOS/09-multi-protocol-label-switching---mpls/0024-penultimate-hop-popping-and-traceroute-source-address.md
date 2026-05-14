## Penultimate hop popping and traceroute source address 

A thorough understanding of penultimate hop behavior and routing is necessary to understand and avoid problems that penultimate hop popping causes to traceroute. 

In the example setup, a regular traceroute from R5 to R1 would yield the following results: 

```
[admin@R5] > /tool traceroute 9.9.9.1
     ADDRESS                                    STATUS
   1         0.0.0.0 timeout timeout timeout
   2         2.2.2.2 37ms 4ms 4ms
                      mpls-label=17
   3         9.9.9.1 4ms 2ms 11ms
```

compared to: 

```
[admin@R5] > /tool traceroute 9.9.9.1 src-address=9.9.9.5
     ADDRESS                                    STATUS
   1         4.4.4.3 15ms 5ms 5ms
                      mpls-label=17
   2         2.2.2.2 5ms 3ms 6ms
                      mpls-label=17
   3         9.9.9.1 6ms 3ms 3ms
```

The reason why the first traceroute does not get a response from R3 is that by default traceroute on R5 uses source address 4.4.4.5 for its probes because it is the preferred source for a route over which next-hop to 9.9.9.1/32 is reachable: 

```
[admin@R5] > /ip route print
Flags: X - disabled, A - active, D - dynamic,
C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme,
B - blackhole, U - unreachable, P - prohibit
 #      DST-ADDRESS        PREF-SRC        G GATEWAY         DISTANCE             INTERFACE
 ...
 3 ADC  4.4.4.0/24         4.4.4.5                           0                    ether1
 ...
 5 ADo  9.9.9.1/32                         r 4.4.4.3         110                  ether1
 ...
```

When the first traceroute probe is transmitted (source: 4.4.4.5, destination 9.9.9.1), R3 drops it and produces an ICMP error message (source 4.4.4.3 destination 4.4.4.5) that is switched all the way to R1. R1 then sends ICMP error back - it gets switched along the label switching path to 4.4.4.5. 

R2 is the penultimate hop popping router for network 4.4.4.0/24 because 4.4.4.0/24 is directly connected to R3. Therefore R2 removes the last label and sends ICMP error to R3 unlabelled: 

```
[admin@R2] > /mpls forwarding-table print
 # IN-LABEL             OUT-LABELS           DESTINATION        INTERFACE            NEXTHOP
 ...
 3 19                                        4.4.4.0/24         ether2               2.2.2.3
 ...
```

R3 drops the received IP packet because it receives a packet with its own address as a source address. ICMP errors produced by following probes come back correctly because R3 receives unlabelled packets with source addresses 2.2.2.2 and 9.9.9.1, which are acceptable to a route. 

Command: 

```
[admin@R5] > /tool traceroute 9.9.9.1 src-address=9.9.9.5
 ...
```

produces expected results, because the source address of traceroute probes is 9.9.9.5. When ICMP errors are traveling back from R1 to R5, the penultimate hop popping for the 9.9.9.5/32 network happens at R3, therefore it never gets to route packet with its own address as a source address.
