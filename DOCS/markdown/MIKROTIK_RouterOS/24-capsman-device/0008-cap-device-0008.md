## CAP device 

Download export of CA certificate from CAPsMAN device to CAP device. In this example fetch is used, however, there are multiple other ways: 

```
/tool fetch address=10.5.138.157 src-path=cert_export_CA.crt user=admin password="123" mode=ftp
```

Import CA certificate from CAPsMAN device in Certificate menu: 

```
/certificate> import file-name=cert_export_CA.crt passphrase=thelongerthebetterpassphrase
```

Add certificate template for CAP: 

```
/certificate
```

```
add name=CAP1 common-name=CAP1
```

Ask CAPsMAN device to grant this certificate with a key using SCEP: 

```
/certificate
```

```
add-scep template=CAP1 scep-url="https://10.5.138.157/scep/CAPsMAN"
```

You will have to return to CAPsMAN device to grant key to this certificate. 

In CAP menu set just created certificate: 

```
/interface wireless cap
set certificate=CAP1
```
