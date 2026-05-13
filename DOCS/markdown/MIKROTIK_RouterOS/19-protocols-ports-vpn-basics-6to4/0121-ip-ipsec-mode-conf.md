## `/ip ipsec mode-conf` 

```
set [find name="rw-conf"] split-include=10.5.8.0/24
```

It is also possible to send a specific DNS server for the client to use. By default, system-dns=yes is used, which sends DNS servers that are configured on the router itself in IP/DNS. We can force the client to use a different DNS server by using the static-dns parameter. 

1214
