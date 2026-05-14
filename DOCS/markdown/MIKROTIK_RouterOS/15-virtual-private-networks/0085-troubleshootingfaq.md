## Troubleshooting/FAQ 

Phase 1 Failed to get a valid proposal 

```
[admin@MikroTik] /log> print
(..)
```

```
17:12:32 ipsec,error no suitable proposal found.
```

```
17:12:32 ipsec,error 10.5.107.112 failed to get valid proposal.
```

```
17:12:32 ipsec,error 10.5.107.112 failed to pre-process ph1 packet (side: 1, status 1).
17:12:32 ipsec,error 10.5.107.112 phase1 negotiation failed.
(..)
```

Peers are unable to negotiate encryption parameters causing the connection to drop. To solve this issue, enable IPSec to debug logs and find out which parameters are proposed by the remote peer, and adjust the configuration accordingly. 

```
[admin@MikroTik] /system logging> add topics=ipsec,!debug
```

1227 

```
[admin@MikroTik] /log> print
```

```
(..)
```

```
17:21:08 ipsec rejected hashtype: DB(prop#1:trns#1):Peer(prop#1:trns#1) = MD5:SHA
```

```
17:21:08 ipsec rejected enctype: DB(prop#1:trns#2):Peer(prop#1:trns#1) = 3DES-CBC:AES-CBC
17:21:08 ipsec rejected hashtype: DB(prop#1:trns#2):Peer(prop#1:trns#1) = MD5:SHA
17:21:08 ipsec rejected enctype: DB(prop#1:trns#1):Peer(prop#1:trns#2) = AES-CBC:3DES-CBC
17:21:08 ipsec rejected hashtype: DB(prop#1:trns#1):Peer(prop#1:trns#2) = MD5:SHA
17:21:08 ipsec rejected hashtype: DB(prop#1:trns#2):Peer(prop#1:trns#2) = MD5:SHA
17:21:08 ipsec,error no suitable proposal found.
17:21:08 ipsec,error 10.5.107.112 failed to get valid proposal.
17:21:08 ipsec,error 10.5.107.112 failed to pre-process ph1 packet (side: 1, status 1).
17:21:08 ipsec,error 10.5.107.112 phase1 negotiation failed.
(..)
```

In this example, the remote end requires SHA1 to be used as a hash algorithm, but MD5 is configured on the local router. Setting before the column symbol (:) is configured on the local side, parameter after the column symbol (:) is configured on the remote side.
