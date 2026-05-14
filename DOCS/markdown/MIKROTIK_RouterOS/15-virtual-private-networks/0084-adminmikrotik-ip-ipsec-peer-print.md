## `[admin@MikroTik] /ip ipsec peer> print` 

```
0 D address=0.0.0.0/0 local-address=0.0.0.0 passive=yes port=500
auth-method=pre-shared-key secret="123" generate-policy=port-strict
exchange-mode=main-l2tp send-initial-contact=yes nat-traversal=yes
hash-algorithm=sha1 enc-algorithm=3des,aes-128,aes-192,aes-256
dh-group=modp1024 lifetime=1d dpd-interval=2m dpd-maximum-failures=5
```

**==> picture [13 x 13] intentionally omitted <==**

Care must be taken if static IPsec peer configuration exists. 

The next step is to create a VPN pool and add some users. 

```
/ip pool add name=vpn-pool range=192.168.99.2-192.168.99.100
```

```
/ppp profile
```

```
set default local-address=192.168.99.1 remote-address=vpn-pool
```

```
/ppp secret
```

```
add name=user1 password=123
add name=user2 password=234
```

Now the router is ready to accept L2TP/IPsec client connections.
