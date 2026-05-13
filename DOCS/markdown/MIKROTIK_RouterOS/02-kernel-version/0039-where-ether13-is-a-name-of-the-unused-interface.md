## Where "ether13" is a name of the unused interface. 

RouterOS utilizes stronger crypto for SSH, most newer programs use it, to turn on SSH strong crypto: 

```
/ip ssh set strong-crypto=yes
```

Following services are disabled by default,  nevertheless, it is better to make sure that none of then were enabled accidentally: 

MikroTik caching proxy, 

```
/ip proxy set enabled=no
```

MikroTik socks proxy, 

```
/ip socks set enabled=no
```

MikroTik UPNP service, 

```
/ip upnp set enabled=no
```

MikroTik dynamic name service or IP cloud, 

```
/ip cloud set ddns-enabled=no update-time=no
```

30
