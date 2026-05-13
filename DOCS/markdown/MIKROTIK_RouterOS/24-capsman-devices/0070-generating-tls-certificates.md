## Generating TLS certificates 

When using secure EAP methods, the client device (supplicant) verifies the identity of the authenication server before sending its own credentials to it. For this to happen, the authentication server needs a TLS certificate. 

This certificate should: 

1.  Be valid and signed by a certificate authority which is trusted by the client device 

2.  Have a fully qualified domain name in the Common Name (CN) and Subject Alt Name fields 

3.  Have the Extended Key Usage attribute indicating that it is authorized for authentcating a TLS server 

4.  Have Validity period of no more than 825 days 

The EAP-TLS method requires the client device to have a TLS certificate (instead of a password). 

To be considered valid by User Manager, a client certificate must: 

1.  Be valid and signed by an authority, which is trusted by the device running User Manager 

2.  Have the user name in the Subject Alt Name (SAN) field. For backward compatibility, you can also add it in the CN field. For more information please see: https://datatracker.ietf.org/doc/html/rfc5216#section-5.2 

Finally, the WPA3 enterprise specification includes an extra secure mode, which provides 192-bit cryptographic security. 

This mode requires using EAP-TLS with certificates that: 

1.  Use either P-384 elliptic curve keys or RSA keys which are at least 3072 bits in length 2.  Use SHA384 as the digest (hashing) algorithm 

For the sake of brevity (and to showcase more of RouterOS' capabilities), this guide will show how to generate all the certificates on the device running User Manager, but in a large scale enterprise environment, the authentication server and client devices would each generate private keys and certificate signing requests locally, then upload CSRs to a certificate authority for signing. 

1530 

Commands executed on device running User Manager 

```
# Generating a Certificate Authority
/certificate
add name=radius-ca common-name="RADIUS CA" key-size=secp384r1 digest-algorithm=sha384 days-valid=1825 key-
usage=key-cert-sign,crl-sign
sign radius-ca ca-crl-host=radius.mikrotik.test
# Generating a server certificate for User Manager
```

```
add name=userman-cert common-name=radius.mikrotik.test subject-alt-name=DNS:radius.mikrotik.test key-
size=secp384r1 digest-algorithm=sha384 days-valid=800 key-usage=tls-server
sign userman-cert ca=radius-ca
```

```
# Generating a client certificate
```

```
add name=maija-client-cert common-name=maija@mikrotik.test key-usage=tls-client days-valid=800 key-
size=secp384r1 digest-algorithm=sha384
sign maija-client-cert ca=radius-ca
# Exporting the public key of the CA as well as the generated client private key and certificate for
distribution to client devices
export-certificate radius-ca file-name=radius-ca
# A passphrase is needed for the export to include the private key
export-certificate maija-client-cert type=pkcs12 export-passphrase="true zebra capacitor ziptie"
```
