## CRS3xx, CRS5xx series, and CCR2116, CCR2216 devices 

**==> picture [13 x 13] intentionally omitted <==**

This paragraph applies to CCR2116, CCR2216 devices, and CRS3xx, CRS5xx series switches. It doesn't apply to CRS1xx/CRS2xx series switches. 

For CRS3xx series switches, it is possible to limit ingress traffic that matches certain parameters with ACL rules and it is possible to limit ingress/egress traffic per port basis. The policer is used for ingress traffic, the shaper is used for egress traffic. The ingress policer controls the received traffic with packet drops. Everything that exceeds the defined limit will get dropped. This can affect the TCP congestion control mechanism on end hosts and the achieved bandwidth can be actually less than defined. The egress shaper tries to queue packets that exceed the limit instead of dropping them. Eventually, it will also drop packets when the output queue gets full, however, it should allow utilizing the defined throughput better. 

Port-based traffic police (ingress) and shaper (egress): 

```
/interface ethernet switch port
set ether1 ingress-rate=10M egress-rate=5M
```
