## Example 

```
[admin@crs326] /interface/ethernet/switch/qos/port> print usage where name=ether2
                 name:  ether2
           packet-cap:     136
           packet-use:       5
             byte-cap:  35 840
             byte-use:   9 472
    queue0-packet-cap:     130
    queue0-packet-use:       1
    queue1-packet-cap:       5
    queue1-packet-use:       4
    queue3-packet-cap:      65
    queue3-packet-use:       2
      queue0-byte-cap:  24 576
      queue0-byte-use:     256
      queue1-byte-cap:   7 680
      queue1-byte-use:   6 144
      queue3-byte-cap:  14 080
      queue3-byte-use:   3 072
```

**==> picture [516 x 172] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name Port name.<br>packet-cap Port's packet capacity. The maximum number of packets that can be enqueued for transmission via the port.<br>packet-use [1] Port's packet usage. The number of packets that are currently enqueued in all port's queues.<br>byte-cap Port's byte capacity (buffer size). The maximum number of bytes that can be enqueued for transmission via the port.<br>byte-use [1] Port's byte usage. The size of hardware buffers (in bytes) that are currently allocated for packets the enqueued packets.<br>Since the buffers are allocated by blocks (usually - 256B each), the allocated buffer size can be bigger than the actual<br>payload.<br>queue0-packet-cap  .. Individual queue capacity. The maximum number of packets that can be enqueued in the respective queues (unless the  S<br>queue7-packet-cap [ 2] hared Buffers are enabled).<br>**----- End of picture text -----**<br>

471 

**==> picture [516 x 200] intentionally omitted <==**

**----- Start of picture text -----**<br>
queue0-shared-packet-cap  Shared queue capacity (individual queue capacity + shared buffers). The maximum number of packets that can be<br>.. queue7-shared-packet- enqueued in the respective queues.<br>cap [2]<br>queue0-packet-use  .. Queue packet usage. The number of enqueued packets in the respective queues.<br>queue7-packet-use [ 2]<br>queue0-byte-cap  ..  queue7- Individual queue capacity. The maximum number of bytes that can be enqueued in the respective queues (unless the  Shar<br>byte-cap [ 2] ed Buffers  are enabled).<br>queue0-shared-byte-cap ..  Shared queue capacity (individual queue capacity + shared buffers). The maximum number of bytes that can be<br>queue7-shared-byte-cap [2] enqueued in the respective queues.<br>queue0-byte-use  ..  queue7- Queue buffer usage (in bytes). The size of hardware buffers (in bytes) that are currently allocated for packets in the<br>byte-use [ 2] respective queues.<br>queue0-byte-max ..  Maximum queue buffer fill level (in bytes). Available only on devices that provide the queue statistics service. Use the  reset<br>queue7-byte-max [2] -counters  command to reset values.<br>**----- End of picture text -----**<br>

> 1 Port's packet/byte usage can exceed the capacity if Shared Buffers are enabled. 

2 Only the queues in use are printed.
