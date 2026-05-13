## `/ip ipsec mode-config` 

```
add address=192.168.66.2 address-prefix-length=32 name=usr_A split-include=192.168.55.0/24 system-dns=no
```

It is possible to apply this configuration for user "A" by using the match-by=certificate parameter and specifying his certificate with remote-certificate.
