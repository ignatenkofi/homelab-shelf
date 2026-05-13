## L2TP Client 

L2TP client setup in the RouterOS is very simple.  In the following example, we already have a preconfigured 3 unit setup. We will take a look more detailed on how to set up L2TP client with username "MT-User", password "StrongPass" and server 192.168.51.3: 

```
[admin@MikroTik] > /interface l2tp-client \
```

```
add connect-to=192.168.51.3 disabled=no name=MT-User password=StrongPass user=MT-User
[admin@MikroTik] > /interface l2tp-client print
```

```
Flags: X - disabled, R - running
```

```
0 R name="MT-User" max-mtu=1450 max-mru=1450 mrru=disabled connect-to=192.168.51.3 user="MT-User"
password="StrongPass" profile=default-encryption keepalive-timeout=60 use-ipsec=no ipsec-secret=""
allow-fast-path=no add-default-route=no dial-on-demand=no allow=pap,chap,mschap1,mschap2
```
