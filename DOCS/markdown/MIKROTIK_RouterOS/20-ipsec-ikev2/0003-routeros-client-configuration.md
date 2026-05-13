## RouterOS client configuration 

For RouterOS to work as L2TP/IPsec client, it is as simple as adding a new L2TP client. 

```
/interface l2tp-client
```

```
add connect-to=1.1.1.1 disabled=no ipsec-secret=mySecret name=l2tp-out1 \
password=123 use-ipsec=yes user=user1
```

It will automatically create dynamic IPsec peer and policy configurations.
