## The configuration of the R2 is shown below: 

```
[admin@MikroTik] interface ipip> add local-address=22.63.11.6 remote-address=10.
0.0.1
[admin@MikroTik] interface ipip> print
Flags: X - disabled, R - running
# NAME MTU LOCAL-ADDRESS REMOTE-ADDRESS
0 X ipip1 1480 22.63.11.6 10.0.0.1
```

```
[admin@MikroTik] interface ipip> enable 0
[admin@MikroTik] interface ipip> /ip address add address=1.1.1.2/24 interface=ipip1
```

Now both routers can ping each other: 

```
[admin@MikroTik] interface ipip> /ping 1.1.1.2
1.1.1.2 64 byte ping: ttl=64 time=24 ms
1.1.1.2 64 byte ping: ttl=64 time=19 ms
1.1.1.2 64 byte ping: ttl=64 time=20 ms
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 19/21.0/24 ms
[admin@MikroTik] interface ipip>
```

1187
