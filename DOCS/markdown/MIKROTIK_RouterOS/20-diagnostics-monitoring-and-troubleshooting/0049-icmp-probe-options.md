## ICMP probe options 

**==> picture [516 x 91] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>packet-interval  (Default:  50ms ) The time between ICMP-request packet send<br>packet-count  (Default:  10 ) Total count of ICMP packets to send out within a single test<br>packet-size  (Default:  54  (IPv4) or  54 The total size of the IP ICMP packet<br>(IPv6))<br>**----- End of picture text -----**<br>

1790 

**==> picture [516 x 232] intentionally omitted <==**

**----- Start of picture text -----**<br>
thr-max  (Default : 1s ) Fail threshold for rtt-max (a value above thr-max is a probe fail)<br>thr-avg  (Default:  100ms ) Fail threshold for rtt-avg (round trip time-avg)<br>thr-stdev  (Default:  250ms ) Fail threshold for rtt-stdev<br>thr-jitter  (Default:  1s ) Fail threshold for rtt-jitter<br>thr-loss-percent  (Default:  85.0% ) Fail threshold for loss-percent<br>thr-loss-count  (Default:  4294967295 ( Fail threshold for loss-count<br>max))<br>ttl  (Default;  255 ) Manually set time to live value for ICMP packet<br>accept-icmp-time-exceeded  (yes | no; If the ICMP "time exceeded" message should be considered a valid response<br>Default  no )<br>early-failure-detection  (no | yes;  Netwatch will not wait to finish all the packets to be processed to change probe status if it is already known that<br>Default:  no ) host will be considered as "down".<br>early-success-detection  (no | yes;  Netwatch will not wait to finish all the packets to be processed to change probe status if it is already known that<br>Default:  no ) host will be considered as "up".<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

`accept-icmp-time-exceeded=yes` can be used together with a manually set low `ttl` value to monitor Internet connectivity, without relying on a specific endpoint. 

For example, you can monitor a public IP address, but that address can filter your ICMP request, or just become unreachable itself, if the Netwatch probe is using this address to monitor Internet connectivity this would cause a false alarm. 

To make sure you can reach the Internet, it's generally enough to make sure you can reach a device a few routing hops away. Low time to live value will expire in transit to the specified host you want to monitor - each router passing the ICMP packet will subtract "1" from TTL value, upon TTL reaching 0, ICMP "time exceeded" packet will be generated, and sent back to the Netwatch probe. If all other fail thresholds are not broken, this response will be considered a success. 

**==> picture [13 x 13] intentionally omitted <==**

When writing Up/Down/Test scripts for Netwatch, use the rtt-* elements instead of the thr-* elements. If the element names differ, their scriptspecific forms are listed in the description. 

**==> picture [13 x 13] intentionally omitted <==**

Simple, ICMP, HTTP, and TCP-connect probes are sent with the "don't fragment" flag set. With an ICMP probe, you can set `packet-size` , which in combination with the DF flag, can be used to aid with path MTU discovery
