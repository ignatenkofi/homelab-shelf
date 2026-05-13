## `/certificate` 

```
add common-name=rw-client1 name=rw-client1 key-usage=tls-client
sign rw-client1 ca=ca
```

PKCS12 format is accepted by most client implementations, so when exporting the certificate, make sure PKCS12 is specified.
