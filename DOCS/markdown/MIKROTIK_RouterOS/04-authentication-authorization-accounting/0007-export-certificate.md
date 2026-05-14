## Export Certificate 

It is possible to export client certificates with keys and CA certificates in two formats - PEM or PCKS12. 

**==> picture [516 x 150] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>export-passphrase  (string Default: none) Passphrase that will be used for exported certificate private key encryption.<br>file-name  (string Default: cert_export_ Exported certificate file name.<br>[Certificate name].crt/key/pkcs12)<br>type  (pem | pkcs12 Default: pem) Exported certificate type.<br>In case of PEM, certificate will be exported with CRT extension, if export-passphrase is specified, also<br>encrypted private KEY file will be exported.<br>In case of PKCS12, certificate will be exported with P12 extension, if export-passphrase is specified,<br>exported certificate will contain encryted private key.<br>**----- End of picture text -----**<br>

```
/certificate
export-certificate CA-Template
export-certificate ServerCA export-passphrase=yourpassphrase
export-certificate Client export-passphrase=yourpassphrase
```

Exported certificates are available under the /file section: 

```
[admin@MikroTik] > file print
Columns: NAME, TYPE, SIZE, CREATION-TIME
#  NAME                         TYPE        SIZE  CREATION-TIME
0  skins                        directory         jan/19/2019 00:00:04
1  flash                        directory         jan/19/2019 01:00:00
2  pub                          directory         jan/19/2019 02:42:16
3  cert_export_CA-Template.crt  .crt file   1119  jan/19/2019 04:15:21
4  cert_export_ServerCA.crt     .crt file   1229  jan/19/2019 04:15:42
5  cert_export_ServerCA.key     .key file   1858  jan/19/2019 04:15:42
6  cert_export_Client.crt       .crt file   1164  jan/19/2019 04:15:55
7  cert_export_Client.key       .key file   1858  jan/19/2019 04:15:55
```

280 

Exporting certificates requires "sensitive" user policy. 

**==> picture [13 x 13] intentionally omitted <==**
