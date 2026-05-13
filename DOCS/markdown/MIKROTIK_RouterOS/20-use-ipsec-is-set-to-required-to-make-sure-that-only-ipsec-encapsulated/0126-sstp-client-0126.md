## SSTP Client 

In the following configuration example, e will create a simple SSTP client without using a certificate: 

```
[admin@MikroTik > interface sstp-client add connect-to=192.168.62.2 disabled=no name=sstp-out1
password=StrongPass profile=default-encryption user=MT-User
```

```
[admin@MikroTik > interface sstp-client print
```

```
Flags: X - disabled; R - running
```

- `0  R name="sstp-out1" max-mtu=1500 max-mru=1500 mrru=disabled connect-to=192.168.62.2:443 http-proxy=0.0.0.0:443 certificate=none verify-server-certificate=no` 

```
      verify-server-address-from-certificate=yes user="MT-User" password="StrongPass"
      profile=default-encryption keepalive-timeout=60 add-default-route=no dial-on-demand=no
      authentication=pap,chap,mschap1,mschap2 pfs=no tls-version=any
```

1266
