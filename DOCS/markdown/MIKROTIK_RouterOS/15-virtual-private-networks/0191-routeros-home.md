## RouterOS Home 

First, we enable the default instance which operates at the VL1 level : 

```
[admin@Home] /zerotier> print
Columns: NAME, PORT, IDENTITY.PUBLIC
# NAME  PORT  IDENTITY.
PUBLIC
```

```
;;; ZeroTier Central controller - https://my.zerotier.com/
0 zt1   9993  879c0b5265:0:
```

```
d5fd2d17805e011d9b93ce8779385e427c8f405e520eea9284809d8444de0335a817xxb21aa4ba153bfbc229ca34d94e08de96d925a4aaa1
9b252da546693a28
```

Now we create a new network via the controller section which will operate at the VL2 level. Each network has its own controller and each network ID is generated from the controller address and controller ID combination. 

Note that we use the private=yes option for a more secure network: 

```
[admin@Home] /zerotier> controller/add name=ZT-private instance=zt1 ip-range=172.27.27.10-172.27.27.20
private=yes routes=172.27.27.0/24
```

```
[admin@Home] /zerotier> controller/print
Columns: INSTANCE, NAME, NETWORK, PRIVATE
# INSTANCE  NAME        NETWORK           PRIVATE
0 zt1       ZT-private  879c0b5265a99e4b  yes
```

1289 

Add our new network under the interface section: 

```
[admin@Home] /zerotier> interface/add network=879c0b5265a99e4b name=myZeroTier instance=zt1
[admin@Home] /zerotier> interface/print interval=1
Columns: NAME, MAC-ADDRESS, NETWORK, STATUS
# NAME        MAC-ADDRESS        NETWORK           STATUS
0 myZeroTier  4A:19:35:6E:00:6E  879c0b5265a99e4b  ACCESS_DENIED
```

Each new peer asks for a controller to join the network, in this situation, we have ACCESS_DENIED status and we have to authorize a new peer, that is because we used the private=yes option. 

After authorization, each member in the network receives information from the controller about new peers and approval they can exchange packets with them: 

```
[admin@Home] /zerotier> controller/member/print
Columns: NETWORK, ZT-ADDRESS
#  NETWORK     ZT-ADDRESS
0  ZT-private  879a0b5265
[admin@Home] /zerotier> controller/member/set 0 authorized=yes
```

Verify newly configured IP address and route: 

```
[admin@Home] /zerotier> /ip/address/print where interface~"Zero"
Flags: D - DYNAMIC
Columns: ADDRESS, NETWORK, INTERFACE
#   ADDRESS          NETWORK      INTERFACE
4 D 172.27.27.15/24  172.27.27.0  myZeroTier
[admin@Home] /zerotier> /ip/route/pr where gateway~"Zero"
Flags: D - DYNAMIC; A - ACTIVE; c, y - COPY
Columns: DST-ADDRESS, GATEWAY, DISTANCE
    DST-ADDRESS     GATEWAY     DISTANCE
DAc 172.27.27.0/24  myZeroTier         0
```
