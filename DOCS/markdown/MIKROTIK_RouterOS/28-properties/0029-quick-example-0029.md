## Quick Example 

RouterOS Ping tool allows you to configure various additional parameters like: 

arp-ping; address; src-address; count; dscp; interface; interval; routing-table; size; ttl; 

Let's take a look ar very simple example: 

```
[admin@MikroTik] > /tool/ping address=10.155.126.252 count=5 interval=200ms
  SEQ HOST                                     SIZE TTL TIME
STATUS
    0 10.155.126.252                             56  64 0ms
    1 10.155.126.252                             56  64 0ms
    2 10.155.126.252                             56  64 0ms
    3 10.155.126.252                             56  64 0ms
    4 10.155.126.252                             56  64 0ms
    sent=5 received=5 packet-loss=0% min-rtt=0ms avg-rtt=0ms max-rtt=0ms
```
