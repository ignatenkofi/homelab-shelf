## RoadWarrior client with NAT 

Consider setup as illustrated below. RouterOS acts as a RoadWarrior client connected to Office allowing access to its internal resources. 

**==> picture [505 x 272] intentionally omitted <==**

A tunnel is established, a local mode-config IP address is received and a set of dynamic policies are generated. 

```
[admin@mikrotik] > ip ipsec policy print
```

```
Flags: T - template, X - disabled, D - dynamic, I - invalid, A - active, * - default
0 T * group=default src-address=::/0 dst-address=::/0 protocol=all proposal=default template=yes
```

```
1 DA src-address=192.168.77.254/32 src-port=any dst-address=10.5.8.0/24 dst-port=any protocol=all
action=encrypt level=unique ipsec-protocols=esp tunnel=yes sa-src-address=10.155.107.8
sa-dst-address=10.155.107.9 proposal=default ph2-count=1
```

```
2 DA src-address=192.168.77.254/32 src-port=any dst-address=192.168.55.0/24 dst-port=any protocol=all
action=encrypt level=unique ipsec-protocols=esp tunnel=yes sa-src-address=10.155.107.8
sa-dst-address=10.155.107.9 proposal=default ph2-count=1
```

Currently, only packets with a source address of 192.168.77.254/32 will match the IPsec policies. For a local network to be able to reach remote subnets, it is necessary to change the source address of local hosts to the dynamically assigned mode config IP address. It is possible to generate source NAT rules dynamically. This can be done by creating a new address list that contains all local networks that the NAT rule should be applied. In our case, it is 192.168.88.0/24. 

1204 

```
/ip firewall address-list add address=192.168.88.0/24 list=local-RW
```

By specifying the address list under the mode-config initiator configuration, a set of source NAT rules will be dynamically generated. 

```
/ip ipsec mode-config set [ find name="request-only" ] src-address-list=local-RW
```

When the IPsec tunnel is established, we can see the dynamically created source NAT rules for each network. Now every host in 192.168.88.0/24 is able to access Office's internal resources. 

```
[admin@mikrotik] > ip firewall nat print
```

```
Flags: X - disabled, I - invalid, D - dynamic
```

```
0 D ;;; ipsec mode-config
```

```
chain=srcnat action=src-nat to-addresses=192.168.77.254 dst-address=192.168.55.0/24 src-address-list=local-RW
```

```
1 D ;;; ipsec mode-config
```

```
chain=srcnat action=src-nat to-addresses=192.168.77.254 dst-address=10.5.8.0/24 src-address-list=local-RW
```
