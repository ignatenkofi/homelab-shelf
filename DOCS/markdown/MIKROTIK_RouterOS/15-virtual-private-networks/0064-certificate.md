## `/certificate` 

```
export-certificate rw-client1 export-passphrase=1234567890 type=pkcs12
```

A file named cert_export_rw-client1.p12 is now located in the routers System/File section. This file should be securely transported to the client's device. 

Typically PKCS12 bundle contains also a CA certificate, but some vendors may not install this CA, so a self-signed CA certificate must be exported separately using PEM format. 

```
/certificate
```

```
export-certificate ca type=pem
```

A file named cert_export_ca.crt is now located in the routers System/File section. This file should also be securely transported to the client's device. 

PEM is another certificate format for use in client software that does not support PKCS12. The principle is pretty much the same. 

```
/certificate
export-certificate ca
export-certificate rw-client1 export-passphrase=1234567890
```

Three files are now located in the routers Files section: cert_export_ca.crt, cert_export_rw-client1.crt and cert_export_rw-client1.key which should be securely transported to the client device.
