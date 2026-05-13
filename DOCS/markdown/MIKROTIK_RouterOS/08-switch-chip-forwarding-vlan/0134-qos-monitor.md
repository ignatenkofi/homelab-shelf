## QoS Monitor 

Command: `/interface/ethernet/switch/qos/monitor` 

473 

Example 

```
[admin@crs312] /interface/ethernet/switch/qos> monitor once
                   total-packet-cap: 11 480
                   total-packet-use: 454
                     total-byte-cap: 3072.0KiB
                     total-byte-use: 681.0KiB
               multicast-packet-cap: 1 148
               multicast-packet-use: 0
                 multicast-byte-cap: 307.0KiB
                 multicast-byte-use: 0
            shared-pool0-packet-cap: 2 296
            shared-pool0-packet-use: 0
            shared-pool3-packet-cap: 2 296
            shared-pool3-packet-use: 190
              shared-pool0-byte-cap: 614.2KiB
              shared-pool0-byte-use: 0
              shared-pool3-byte-cap: 614.2KiB
              shared-pool3-byte-use: 610.5KiB
                    wred-packet-cap: 512
                      wred-byte-cap: 128.0KiB
```

**==> picture [516 x 442] intentionally omitted <==**

**----- Start of picture text -----**<br>
Monitors hardware QoS resources.<br>Property Description<br>total-packet-cap  (in Total packet capacity. The maximum number of hardware packet descriptors that the device can store is all queues.<br>teger)<br>total-packet-use  (in Total packet usage. The current number of packet descriptors residing in the hardware memory.<br>teger)<br>total-byte-cap  (byte) Total tx memory capacity.<br>total-byte-use  (byte) Total tx memory usage. The current number of bytes occupied by the packets in all tx queues.<br>multicast-packet- Multicast packet capacity. The maximum number of hardware packet descriptors that can be used by multicast/broadcast traffic.<br>cap  (integer) Depends on the  multicast-buffers  setting.<br>multicast-packet- Multicast packet usage. The hardware makes a copy of the packet descriptor for each multicast destination.<br>use  (integer)<br>mirror-ingress- Ingress mirror packet capacity. The maximum number of hardware packet descriptors that can be used by ingress mirrored traffic.<br>packet-cap  (intege Depends on the  mirror-buffers  setting.<br>r)<br>mirror-ingress- Ingress mirror packet usage.<br>packet-use  (intege<br>r)<br>mirror-ingress- Ingress mirror byte capacity. Depends on the  mirror-buffers  setting.<br>byte-cap  (byte)<br>mirror-ingress- Ingress mirror byte usage.<br>byte-use  (byte)<br>mirror-egress- Egress mirror packet capacity. The maximum number of hardware packet descriptors that can be used by egress mirrored traffic.<br>packet-cap  (intege Depends on the  mirror-buffers  setting.<br>r)<br>mirror-egress- Egress mirror packet usage.<br>packet-use  (intege<br>r)<br>mirror-egress-byte- Egress mirror byte capacity. Depends on the  mirror-buffers  setting.<br>cap  (byte)<br>**----- End of picture text -----**<br>


474 

**==> picture [516 x 361] intentionally omitted <==**

**----- Start of picture text -----**<br>
mirror-egress-byte- Egress mirror byte usage.<br>use  (byte)<br>shared-packet-cap Shared packet capacity. The maximum number of hardware packet descriptors that can be shared between ports and tx queues.<br>(integer) Depends on the  shared-buffers  setting.<br>shared-packet-use Shared packet usage. The current number of shared packet descriptors used by all tx queues.<br>(integer)<br>shared-byte-cap  (b Shared tx memory capacity. Depends on the  shared-buffers  setting.<br>yte)<br>shared-byte-use  (b Shared tx memory usage. The current number of shared buffers occupied by the packets in all tx queues.<br>yte)<br>shared-pool0- Shared packet capacity of each shared pool. Only the shared pools in use are displayed. These fields are omitted if the device<br>packet-cap ..  does not support multiple shared pools.<br>shared-pool7-<br>packet-cap<br>(integer)<br>shared-pool0- Per-pool shared packet usage. Only the shared pools in use are displayed. These fields are omitted if the device does not support<br>packet-use ..  multiple shared pools.<br>shared-pool7-<br>packet-use<br>(integer)<br>wred-packet-cap  (i The maximum packet count that a queue can use above the shared cap (" queueX-shared-packet-cap " in " /in/eth/sw/qos<br>nteger) /port print usage ") to trigger a random tail drop. For example, if " queue1-shared-packet-cap=3072 " and " wred-<br>packet-cap=512 ", WRED triggers when  queue1-packet-use  exceeds 3072, reaching 100% drop rate at 3072+512=3584<br>packets.<br>wred-byte-cap  (inte The maximum byte count that a queue can use above the shared cap (" queueX-shared-byte-cap ") to trigger a random tail<br>ger) drop. For example, if " queue1-shared-byte-cap=768KiB " and " wred-byte-cap=128KiB ", WRED triggers when  queue1-<br>packet-use exceeds 768KiB, reaching 100% drop rate at 768+128=896KiB.<br>**----- End of picture text -----**<br>
