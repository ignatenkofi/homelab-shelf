## The same we can achieve with more shorter CLI command: 

```
[admin@MikroTik] > /ping 10.155.126.252 count=5 interval=50ms
  SEQ HOST                                     SIZE TTL TIME
STATUS
    0 10.155.126.252                             56  64 0ms
    1 10.155.126.252                             56  64 0ms
    2 10.155.126.252                             56  64 0ms
    3 10.155.126.252                             56  64 0ms
    4 10.155.126.252                             56  64 0ms
    sent=5 received=5 packet-loss=0% min-rtt=0ms avg-rtt=0ms max-rtt=0ms
```

It is also possible to ping multicast address to discover all hosts belonging to multicast group: 

1800 

```
[admin@MikroTik] > /ping ff02::1
HOST                                    SIZE  TTL TIME  STATUS
fe80::20c:42ff:fe49:fceb                56    64  1ms   echo reply
fe80::20c:42ff:fe72:a1b0                56    64  1ms   echo reply
fe80::20c:42ff:fe28:7945                56    64  1ms   echo reply
fe80::21a:4dff:fe5d:8e56                56    64  3ms   echo reply
    sent=1 received=4 packet-loss=-300% min-rtt=1ms avg-rtt=1ms max-rtt=3ms
```
