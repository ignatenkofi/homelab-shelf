## CAPsMAN device: 

In Certificate menu add certificate templates for CA certificate and CAPsMAN server certificate: 

```
/certificate
add name=CA-temp common-name=CA
add name=CAPsMAN-temp common-name=CAPsMAN
```

Now Sign the certifiace templates. First Sign the CA certificate and use CAPsMAN device IP as CA CRL Host: 

```
/certificate
sign CA-temp ca-crl-host=10.5.138.157 name=CA
sign CAPsMAN-temp ca=CA name=CAPsMAN
```

1489 

Alternatively, previous two steps can be done with auto setting in Certificate and CA-Certificate option in CAPsMAN Manager menu, see the Fast and easy configuration. 

Export CA certificate. You will have to Import it on CAP device. You can use Download -> Drag&Drop to CAP device, in this example fetch command is used later from CAP device. Using long passphrase is advisable - longer passphrase will take longer to crack if it gets into the wrong hands: 

```
/certificate
```

```
export-certificate CA export-passphrase=thelongerthebetterpassphrase
```

Create SCEP server which will be used to issue and grant certificates to CAP devices: 

```
/certificate scep-server
```

```
add ca-cert=CA path=/scep/CAPsMAN
```

Set certificates in CAPsMAN Manager menu and set Require Peer Certificate to yes: 

```
/caps-man manager
```

```
set ca-certificate=CA certificate=CAPsMAN
set require-peer-certificate=yes
```

At this point, only CAPs with a valid certificate will be able to connect.
