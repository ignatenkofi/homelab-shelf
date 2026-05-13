## Applications 

Multiple applications can be run over the RoMON network. 

In order to test the reachability of specific router on RoMON network RoMON ping command can be used: 

```
[admin@MikroTik] > /tool/romon/ping id=6C:3B:6B:48:0E:8B count=5
  SEQ HOST                                    TIME  STATUS
    0 6C:3B:6B:48:0E:8B                       1ms
    1 6C:3B:6B:48:0E:8B                       0ms
    2 6C:3B:6B:48:0E:8B                       1ms
    3 6C:3B:6B:48:0E:8B                       0ms
    4 6C:3B:6B:48:0E:8B                       1ms
    sent=5 received=5 packet-loss=0% min-rtt=0ms avg-rtt=0ms max-rtt=1ms
```

In order to establish a secure terminal connection to router on RoMON network RoMON SSH command can be used: 

```
[admin@MikroTik] > /tool/romon/ssh 6C:3B:6B:48:0E:8B
```
