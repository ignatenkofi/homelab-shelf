## `/ppp profile` 

```
set default-encryption local-address=192.168.99.1 remote-address=vpn-pool
```

Enable the use of RADIUS for PPP authentication. 

347 

```
/ppp aaa
set use-radius=yes
```

Enable the L2TP server with IPsec encryption. 

```
/interface l2tp-server server
```

```
set enabled=yes use-ipsec=required ipsec-secret=mySecret
```

That is it. Your router is now ready to accept L2TP/IPsec connections and authenticate them to the internal User Manager.
