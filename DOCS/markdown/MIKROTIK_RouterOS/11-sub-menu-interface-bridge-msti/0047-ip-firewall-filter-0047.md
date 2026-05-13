## `/ip firewall filter` 

```
add action=accept chain=input comment="default configuration" connection-state=established,related
```

Now we can proceed by accepting some new connections, in our example we want to allow access ICMP protocol from any address and everything else only from 192.168.88.2-192.168.88.254 address range. For that we create an address list and two firewall rules. 

```
/ip firewall address-list
```

```
add address=192.168.88.2-192.168.88.254 list=allowed_to_router
/ip firewall filter
add action=accept chain=input src-address-list=allowed_to_router
add action=accept chain=input protocol=icmp
```

And lastly we drop everything else: 

```
add action=drop chain=input
```

Complete set of just created rules:
