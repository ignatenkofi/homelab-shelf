## Ping by DNS name: 

```
[admin@MikroTik]  > /ping www.google.com count=5 interval=50ms
  SEQ HOST                                     SIZE TTL TIME
STATUS
    0 216.58.207.228                             56  51 14ms
    1 216.58.207.228                             56  51 13ms
    2 216.58.207.228                             56  51 13ms
    3 216.58.207.228                             56  51 13ms
    4 216.58.207.228                             56  51 13ms
    sent=5 received=5 packet-loss=0% min-rtt=13ms avg-rtt=13ms max-rtt=14ms
```

**==> picture [13 x 13] intentionally omitted <==**

When you use the domain name and CLI for ping, router DNS will be used to resolve the address. When you use the Winbox Tools/Ping, your computer's DNS will be used to resolve the given address.
