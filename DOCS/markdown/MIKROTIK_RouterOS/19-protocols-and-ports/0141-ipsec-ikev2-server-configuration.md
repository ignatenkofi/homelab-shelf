## IPsec (IKEv2) server configuration 

Add a new Phase 1 profile and Phase 2 proposal entries with pfs-group=none: 

```
/ip ipsec profile
add name=ike2
/ip ipsec proposal
add name=ike2 pfs-group=none
```

Mode config is used for address distribution from IP/Pools. 

```
/ip pool
add name=ike2-pool ranges=192.168.77.2-192.168.77.254
/ip ipsec mode-config
add address-pool=ike2-pool address-prefix-length=32 name=ike2-conf
```

Since that the policy template must be adjusted to allow only specific network policies, it is advised to create a separate policy group and template. 

```
/ip ipsec policy group
add name=ike2-policies
/ip ipsec policy
add dst-address=192.168.77.0/24 group=ike2-policies proposal=ike2 src-address=0.0.0.0/0 template=yes
```

Create a new IPsec peer entry which will listen to all incoming IKEv2 requests. 

```
/ip ipsec peer
```

```
add exchange-mode=ike2 name=ike2 passive=yes profile=ike2
```

Lastly create a new IPsec identity entry that will match all clients trying to authenticate with EAP. Note that generated Let's Encrypt certificate must be specified. 

1225
