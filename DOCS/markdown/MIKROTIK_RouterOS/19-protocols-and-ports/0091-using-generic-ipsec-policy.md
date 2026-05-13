## Using generic IPsec policy 

The trick of this method is to add a default policy with an action drop. Let's assume we are running an L2TP/IPsec server on a public 1.1.1.1 address and we want to drop all nonencrypted L2TP: 

```
/ip ipsec policy
```

```
add src-address=1.1.1.1 dst-address=0.0.0.0/0 sa-src-address=1.1.1.1 protocol=udp src-port=1701 tunnel=yes
action=discard
```

1205 

Now router will drop any L2TP unencrypted incoming traffic, but after a successful L2TP/IPsec connection dynamic policy is created with higher priority than it is on default static rule, and packets matching that dynamic rule can be forwarded. 

**==> picture [13 x 13] intentionally omitted <==**

Policy order is important! For this to work, make sure the static drop policy is below the dynamic policies. Move it below the policy template if necessary. 

```
[admin@rack2_10g1] /ip ipsec policy> print
```

```
Flags: T - template, X - disabled, D - dynamic, I - inactive, * - default
```

```
0 T * group=default src-address=::/0 dst-address=::/0 protocol=all
```

```
proposal=default template=yes
```

```
1 D src-address=1.1.1.1/32 src-port=1701 dst-address=10.5.130.71/32
```

```
dst-port=any protocol=udp action=encrypt level=require
ipsec-protocols=esp tunnel=no sa-src-address=1.1.1.1
```

```
sa-dst-address=10.5.130.71
```

```
2 src-address=1.1.1.1/32 src-port=1701 dst-address=0.0.0.0/0
```

```
dst-port=any protocol=udp action=discard level=unique
ipsec-protocols=esp tunnel=yes sa-src-address=1.1.1.1
sa-dst-address=0.0.0.0 proposal=default manual-sa=none
```
