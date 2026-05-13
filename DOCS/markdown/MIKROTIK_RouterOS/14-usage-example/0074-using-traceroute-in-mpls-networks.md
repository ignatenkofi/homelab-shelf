## Using traceroute in MPLS networks 

RFC4950 introduces extensions to the ICMP protocol for MPLS. The basic idea is that some ICMP messages may carry an MPLS "label stack object" (a list of labels that were on the packet when it caused a particular ICMP message). ICMP messages of interest for MPLS are Time Exceeded and Need Fragment. 

MPLS label carries not only label value, but also TTL field. When imposing a label on an IP packet, MPLS TTL is set to value in the IP header, when the last label is removed from the IP packet, IP TTL is set to value in MPLS TTL. Therefore MPLS switching network can be diagnosed by means of a traceroute tool that supports MPLS extension. 

For example, the traceroute from R4 to R1 looks like this: 

```
[admin@R1] /mpls/ldp/neighbor> /tool traceroute 111.111.111.4 src-address=111.111.111.1
Columns: ADDRESS, LOSS, SENT, LAST, AVG, BEST, WORST, STD-DEV, STATUS
#  ADDRESS        LOSS  SENT  LAST   AVG  BEST  WORST  STD-DEV  STATUS
1  111.11.0.2     0%       2  0.7ms  0.7  0.7   0.7          0  <MPLS:L=19,E=0>
2  111.12.0.2     0%       2  0.4ms  0.4  0.4   0.4          0  <MPLS:L=19,E=0>
3  111.111.111.4  0%       2  0.5ms  0.5  0.5   0.5          0
```

Traceroute results show MPLS labels on the packet when it produced ICMP Time Exceeded. The above means: that when R3 received a packet with MPLS TTL 1, it had label 18 on it. This match advertised label by R3 for 111.111.111.4. In the same way, R2 observed label 17 on the packet on the next traceroute iteration - R3 switched label 17 to label 17, as explained above. R1 received packet without labels - R2 did penultimate hop popping as explained above.
