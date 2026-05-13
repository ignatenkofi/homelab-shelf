## `/ipv6 route` 

```
add comment="" disabled=no distance=1 dst-address=2000::/3 gateway=2001:470:27:37e::1 scope=30 target-scope=10
/ipv6 address
```

```
add address=2001:470:27:37e::2/64 advertise=no disabled=no eui-64=no interface=sit1
```

These commands will setup the tunnel itself - the router will be able to connect to IPv6 hosts, but end-user devices (computers, tablets, phones) will not yet have IPv6 connectivity. 

To be able to assign IPv6 addresses to your clients you have to add the Routed IPv6 Prefix to your internal interface (by default bridge-local). 

```
/ipv6 address add address=2001:470:28:37e:: interface=bridge-local advertise=yes
```

Enable DNS server advertising through network discovery 

```
/ipv6 nd set [ find default=yes ] advertise-dns=yes
```

1177 

And finally add IPv6 DNS servers (these are Google public DNS servers, you can also use the one which is provided by Hurricane Electric - 2001:470:20:: 2). 

```
/ip dns set allow-remote-requests=yes servers=2001:4860:4860::8888,2001:4860:4860::8844
```

Afterwards enable IPv6 on your device and you should have IPv6 connectivity. http://ipv6-test.com can be used to test IPv6 connectivity. 

1178
