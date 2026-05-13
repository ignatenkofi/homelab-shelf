## Quick Setup Guide 

Let us assume that we have two Ethernet interfaces on each router (Router1 and Router2) and want to get the maximum data rate between these two routers. To make this possible, follow these steps: 

1.  Make sure that you do not have IP addresses on interfaces that will be enslaved for bonding interface. 

2.  Add bonding interface and IP address on the Router1: 

```
/interface bonding add slaves=ether1,ether2 name=bond1
```

```
/ip address add address=172.16.0.1/24 interface=bond1
```

3.  Do the same thing on the Router2: 

764 

```
/interface bonding add slaves=ether1,ether2 name=bond1
/ip address add address=172.16.0.2/24 interface=bond1
```

4.  Test the link from Router1: 

```
[admin@Router1] > ping 172.16.0.2
  SEQ HOST                                 SIZE TTL TIME  STATUS
    0 172.16.0.2                             56  64 0ms
    1 172.16.0.2                             56  64 0ms
    2 172.16.0.2                             56  64 0ms
    sent=3 received=3 packet-loss=0% min-rtt=0ms avg-rtt=0ms max-rtt=0ms
```

**==> picture [13 x 13] intentionally omitted <==**

The bonding interface needs a couple of seconds to get connectivity with its peers.
