## Explicit Congestion Notification (ECN) 

Some switch chips can perform ECN marking of IP packets on the hardware level, according to RFC 3168. Hardware ECN marking is based on the WRED mechanism, but instead of dropping IP packets, they are marked with CE (Congestion Experienced, binary 11) in the ECN field (two least significant bits in IPv4/TOS or IPv6/TrafficClass octet). Only ECN-Capable IP packets may be marked - those with the ECN field value of ECT(1) or ECT(0)  (binary 01 or 10, respectively). Not ECN-Capable Transport packets (ECN=00) never get marked. If a packet already has the CE mark (ECN=11), it never gets cleared, even if the device does not experience congestion. 

Set ecn=yes on Tx Manager Queue to enable ECN marking. 

**==> picture [13 x 13] intentionally omitted <==**

ECN marking mechanism requires the respective Tx queues to use shared buffers ( use-shared-buffers=yes) . 

The packet receives the CE mark if all conditions below are met: 

1.  The packet is either IPv4 or IPv6. 2.  The ECN field value in IP header is either ECT(1) or ECT(0). 3.  Egress port's Tx Queue has ecn=yes and uses shared buffers ( use-shared-buffers=yes ). 4. `queueX-packet-use > queueX-shared-packet-cap` or `queueX-byte-use > queueX-shared-byte-cap` . 

**==> picture [13 x 13] intentionally omitted <==**

Since enabling ECN (ecn=yes) prevents ECN-capable packet drop, queue usage may exceed WRED thresholds if the traffic sender doesn't react to congestion notification in time.
