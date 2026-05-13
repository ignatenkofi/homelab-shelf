## RouterOS server configuration 

The first step is to enable the L2TP server: 

1226 

```
/interface l2tp-server server
```

```
set enabled=yes use-ipsec=required ipsec-secret=mySecret default-profile=default
```
