## `/ip ipsec profile` 

```
add dh-group=ecp256,modp2048,modp1024 enc-algorithm=aes-256,aes-192,aes-128 name=ike2
/ip ipsec proposal
```

```
add auth-algorithms=null enc-algorithms=aes-128-gcm name=ike2-gre pfs-group=none
```

Next, create a new mode config entry with responder=yes. This will provide an IP configuration for the other site as well as the host (loopback address) for policy generation.
