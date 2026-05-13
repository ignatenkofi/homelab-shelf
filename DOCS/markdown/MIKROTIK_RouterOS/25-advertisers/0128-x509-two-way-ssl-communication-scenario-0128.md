## X.509 (two-way SSL communication) scenario 

Drag-and-drop the certificates into the router's "Files/File List" menu →  server certificate, client certificate, and its private key. 

Import certificates one by one: 

1656 

```
/certificate/import file-name=mqttserver.pem passphrase=""
/certificate/import file-name=cert.pem passphrase=""
```

```
/certificate/import file-name=key.pem passphrase=""
```
