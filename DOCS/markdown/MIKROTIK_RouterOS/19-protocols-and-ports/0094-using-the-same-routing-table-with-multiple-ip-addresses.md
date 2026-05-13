## Using the same routing table with multiple IP addresses 

Consider the following example. There are multiple IP addresses from the same subnet on the public interface. Masquerade rule is configured on outinterface. It is necessary to use one of the IP addresses explicitly. 

```
[admin@pair_r1] > /ip address print
Flags: X - disabled, I - invalid, D - dynamic
# ADDRESS NETWORK INTERFACE
0 192.168.1.1/24 192.168.1.0 bridge-local
1 172.22.2.1/24 172.22.2.0 ether1
2 172.22.2.2/24 172.22.2.0 ether1
3 172.22.2.3/24 172.22.2.0 ether1
```

```
[admin@pair_r1] > /ip route print
Flags: X - disabled, A - active, D - dynamic, C - connect, S - static, r - rip, b - bgp, o - ospf, m - mme, B -
blackhole, U - unreachable, P - prohibit
# DST-ADDRESS PREF-SRC GATEWAY DISTANCE
1 A S 0.0.0.0/0 172.22.2.115 1
3 ADC 172.22.2.0/24 172.22.2.1 ether1 0
4 ADC 192.168.1.0/24 192.168.1.1 bridge-local 0
```

```
[admin@pair_r1] /ip firewall nat> print
Flags: X - disabled, I - invalid, D - dynamic
0 chain=srcnat action=masquerade out-interface=ether1 log=no log-prefix=""
```

IPsec peer and policy configuration is created using one of the public IP addresses. 

```
/ip ipsec peer
add address=10.155.130.136/32 local-address=172.22.2.3 secret=test
/ip ipsec policy
add sa-src-address=172.22.2.3 src-address=192.168.1.0/24 dst-address=172.16.0.0/24 sa-dst-address=10.
155.130.136 tunnel=yes
/ip firewall nat
```

```
add action=accept chain=srcnat src-address=192.168.1.0/24 dst-address=172.16.0.0/24 place-before=0
```

Currently, the phase 1 connection uses a different source address than we specified, and "phase1 negotiation failed due to time up" errors are shown in the logs. This is because masquerade is changing the source address of the connection to match the pref-src address of the connected route. The solution is to exclude connections from the public IP address from being masqueraded. 

```
/ip firewall nat
```

```
add action=accept chain=srcnat protocol=udp src-port=500,4500 place-before=0
```

1207
