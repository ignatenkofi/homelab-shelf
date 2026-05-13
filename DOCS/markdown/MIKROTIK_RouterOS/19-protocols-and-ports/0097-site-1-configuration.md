## Site 1 configuration 

Start off by creating a new Phase 1profileand Phase 2proposalentries using stronger or weaker encryption parameters that suit your needs. It is advised to create separate entries for each menu so that they are unique for each peer in case it is necessary to adjust any of the settings in the future. These parameters must match between the sites or else the connection will not establish. 

```
/ip ipsec profile
add dh-group=modp2048 enc-algorithm=aes-128 name=ike1-site2
/ip ipsec proposal
add enc-algorithms=aes-128-cbc name=ike1-site2 pfs-group=modp2048
```

Continue by configuring a peer. Specify the address of the remote router. This address should be reachable through UDP/500 and UDP/4500 ports, so make sure appropriate actions are taken regarding the router's firewall. Specify the name for this peer as well as the newly created profile. 

```
/ip ipsec peer
```

```
add address=192.168.80.1/32 name=ike1-site2 profile=ike1-site2
```

The next step is to create an identity. For a basic pre-shared key secured tunnel, there is nothing much to set except for a strong secret and the peer to which this identity applies. 

```
/ip ipsec identity
add peer=ike1-site2 secret=thisisnotasecurepsk
```

**==> picture [13 x 13] intentionally omitted <==**

If security matters, consider using IKEv2 and a different auth-method. 

1208 

Lastly, create a policy that controls the networks/hosts between whom traffic should be encrypted.
