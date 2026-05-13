## Certificate Template 

Certificate templates are used to prepare a desired certificate for signing. 

Certificate template is deleted right after a certificate is signed or a certificate request command is executed 

```
/certificate
```

```
add name=CA-Template common-name=CAtemp key-usage=key-cert-sign,crl-sign
add name=Server common-name=server
```

```
add name=Client common-name=client
```

To print out certificates: 

```
[admin@4k11] /certificate> print detail
Flags: K - private-key; L - crl; C - smart-card-key; A - authority; I - issued, R - revoked; E - expired; T -
trusted
 0         name="CA-Template" key-type=rsa common-name="CAtemp" key-size=2048 subject-alt-name="" days-
valid=365 key-usage=key-cert-sign,crl-sign
```

```
 1         name="Server" key-type=rsa common-name="server" key-size=2048 subject-alt-name="" days-valid=365
           key-usage=digital-signature,key-encipherment,data-encipherment,key-cert-sign,crl-sign,tls-server,tls-
client
```

```
 2         name="Client" key-type=rsa common-name="client" key-size=2048 subject-alt-name="" days-valid=365
           key-usage=digital-signature,key-encipherment,data-encipherment,key-cert-sign,crl-sign,tls-server,tls-
client
```
