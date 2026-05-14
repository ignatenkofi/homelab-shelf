## Site 2 configuration 

Office 2 configuration is almost identical to Office 1 with proper IP address configuration. Start off by creating a new Phase 1 profile and Phase 2 proposal e ntries: 

```
/ip ipsec profile
add dh-group=modp2048 enc-algorithm=aes-128 name=ike1-site1
/ip ipsec proposal
add enc-algorithms=aes-128-cbc name=ike1-site1 pfs-group=modp2048
```

Next is the peer and identity: 

```
/ip ipsec peer
add address=192.168.90.1/32 name=ike1-site1 profile=ike1-site1
/ip ipsec identity
add peer=ike1-site1 secret=thisisnotasecurepsk
```

When it is done, create a policy: 

```
/ip ipsec policy
```

```
add src-address=10.1.101.0/24 src-port=any dst-address=10.1.202.0/24 dst-port=any tunnel=yes action=encrypt
proposal=ike1-site1 peer=ike1-site1
```

At this point, the tunnel should be established and two IPsec Security Associations should be created on both routers: 

```
/ip ipsec
active-peers print
installed-sa print
```
