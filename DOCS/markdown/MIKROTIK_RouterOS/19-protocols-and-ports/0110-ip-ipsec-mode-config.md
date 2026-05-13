## `/ip ipsec mode-config` 

```
add address=192.168.99.2 address-prefix-length=32 name=ike2-gre split-include=192.168.99.1/32 system-dns=no
```

It is advised to create a new policy group to separate this configuration from any existing or future IPsec configuration. 

```
/ip ipsec policy group
add name=ike2-gre
```

Now it is time to set up a new policy template that will match the remote peers new dynamic address and the loopback address. 

```
/ip ipsec policy
```

```
add dst-address=192.168.99.2/32 group=ike2-gre proposal=ike2-gre src-address=192.168.99.1/32 template=yes
```

The next step is to create a peer configuration that will listen to all IKEv2 requests. If you already have such an entry, you can skip this step. 

```
/ip ipsec peer
```

```
add exchange-mode=ike2 name=ike2 passive=yes profile=ike2
```

Lastly, set up an identity that will match our remote peer by pre-shared-key authentication with a specific secret.
