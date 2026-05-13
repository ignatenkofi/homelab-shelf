## (Optional) Split tunnel configuration 

Split tunneling is a method that allows road warrior clients to only access a specific secured network and at the same time send the rest of the traffic based on their internal routing table (as opposed to sending all traffic over the tunnel). To configure split tunneling, changes to mode config parameters are needed. 

For example, we will allow our road warrior clients to only access the 10.5.8.0/24 network. 

```
/ip ipsec mode-conf
```

```
set [find name="rw-conf"] split-include=10.5.8.0/24
```

It is also possible to send a specific DNS server for the client to use. By default, system-dns=yes is used, which sends DNS servers that are configured on the router itself in IP/DNS. We can force the client to use a different DNS server by using the static-dns parameter.
