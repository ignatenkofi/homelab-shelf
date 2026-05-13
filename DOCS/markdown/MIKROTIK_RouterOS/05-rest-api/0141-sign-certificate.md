## Sign Certificate 

Certificates should be signed. In the following example, we will sign certificates and add CRL URL for the server certificate: 

279 

```
/certificate
sign CA-Template
sign Client
sign Server ca-crl-host=192.168.88.1 name=ServerCA
```
