## PPTP Client 

The following example demonstrates how to set up a PPTP client with username "MT-User", password "StrongPass" and server 192.168.62.2: 

```
[admin@MikroTik] > interface pptp-client add connect-to=192.168.62.2 disabled=no name=pptp-out1
password=StrongPass user=MT-User
```

```
[admin@MikroTik] > interface pptp-client print
Flags: X - disabled; R - running
```

1261 

- `0  R name="pptp-out1" max-mtu=1450 max-mru=1450 mrru=disabled connect-to=192.168.62.2 user="MT-User"` 

   - `password="StrongPass" profile=default-encryption keepalive-timeout=60 add-default-route=no dial-on-demand=no allow=pap,chap,mschap1,mschap2`
