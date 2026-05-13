## Using different routing table 

IPsec, as any other service in RouterOS, uses the main routing table regardless of what local-address parameter is used for Peer configuration. It is necessary to apply routing marks to both IKE and IPSec traffic. 

Consider the following example. There are two default routes - one in the main routing table and another in the routing table "backup". It is necessary to use the backup link for the IPsec site to site tunnel. 

```
[admin@pair_r1] > /ip route print detail
```

```
Flags: X - disabled, A - active, D - dynamic, C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme, B -
blackhole, U - unreachable, P - prohibit
```

```
0 A S dst-address=0.0.0.0/0 gateway=10.155.107.1 gateway-status=10.155.107.1 reachable via ether1 distance=1
scope=30 target-scope=10 routing-mark=backup
```

```
1 A S dst-address=0.0.0.0/0 gateway=172.22.2.115 gateway-status=172.22.2.115 reachable via ether2 distance=1
scope=30 target-scope=10
```

```
2 ADC dst-address=10.155.107.0/25 pref-src=10.155.107.8 gateway=ether1 gateway-status=ether1 reachable
distance=0 scope=10
```

```
3 ADC dst-address=172.22.2.0/24 pref-src=172.22.2.114 gateway=ether2 gateway-status=ether2 reachable distance=0
scope=10
```

```
4 ADC dst-address=192.168.1.0/24 pref-src=192.168.1.1 gateway=bridge-local gateway-status=ether2 reachable
distance=0 scope=10
```

```
[admin@pair_r1] > /ip firewall nat print
```

```
Flags: X - disabled, I - invalid, D - dynamic
```

```
0 chain=srcnat action=masquerade out-interface=ether1 log=no log-prefix=""
```

```
1 chain=srcnat action=masquerade out-interface=ether2 log=no log-prefix=""
```

IPsec peer and policy configurations are created using the backup link's source address, as well as the NAT bypass rule for IPsec tunnel traffic. 

1206 

```
/ip ipsec peer
```

```
add address=10.155.130.136/32 local-address=10.155.107.8 secret=test
/ip ipsec policy
```

```
add sa-src-address=10.155.107.8 src-address=192.168.1.0/24 dst-address=172.16.0.0/24 sa-dst-address=10.
155.130.136 tunnel=yes
/ip firewall nat
```

```
add action=accept chain=srcnat src-address=192.168.1.0/24 dst-address=172.16.0.0/24 place-before=0
```

Currently, we see "phase1 negotiation failed due to time up" errors in the log. It is because IPsec tries to reach the remote peer using the main routing table with an incorrect source address. It is necessary to mark UDP/500, UDP/4500, and ipsec-esp packets using Mangle: 

```
/ip firewall mangle
```

```
add action=mark-connection chain=output connection-mark=no-mark dst-address=10.155.130.136 dst-port=500,4500
new-connection-mark=ipsec passthrough=yes protocol=udp
```

```
add action=mark-connection chain=output connection-mark=no-mark dst-address=10.155.130.136 new-connection-
mark=ipsec passthrough=yes protocol=ipsec-esp
```

```
add action=mark-routing chain=output connection-mark=ipsec new-routing-mark=backup passthrough=no
```
