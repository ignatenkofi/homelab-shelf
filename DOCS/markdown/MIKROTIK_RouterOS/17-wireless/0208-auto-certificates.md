## Auto Certificates 

To simplify CAPsMAN and CAP configuration when certificates are required (e.g. for automatic locking feature), CAPsMAN can be configured to generate necessary certificates automatically and CAP can be configured to request certificate from CAPsMAN. 

Automatic certificates do not provide full public key infrastructure and are provided for simple setups. If more complicated PKI is necessary - supporting proper certificate validity periods, multiple-level CA certificates, certificate renewal - other means must be used, such as manual certificate distribution or SCEP. 

CAPsMAN has the following certificate settings: 

- certificate - this is CAPsMAN certificate, private key must be available for this certificate. If set to none , CAPsMAN will operate in no-certificate mode and none of certificate requiring features will work. If set to auto , CAPsMAN will attempt to issue certificate to itself using CA certificate (see ca-certificate description). Note that CommonName automatically issued certificate will be "CAPsMAN-<mac address>" and validity period for will be the same as for CA certificate. 

- ca-certificate - this is CA certificate that CAPsMAN will use when issuing certificate for itself if necessary (see certificate description) and when signing certificate requests from CAPs. If set to none , CAPsMAN will not be able to issue certificate to itself or sign certificate requests from CAPs. If set to auto , CAPsMAN will generate self-signed CA certificate to use as CA certificate. CommonName for this certificate will take form "CAPsMAN-CA-<mac address>" and validity period will be from jan/01/1970 until jan/18/2038. 

When CAPsMAN will auto-generate certificates, this will be reflected like this: 

```
[admin@CM] /caps-man manager> pr
                  enabled: yes
              certificate: auto
           ca-certificate: auto
 require-peer-certificate: no
    generated-certificate: CAPsMAN-000C424C30F3
 generated-ca-certificate: CAPsMAN-CA-000C424C30F3
```

And certificates: 

1477 

```
[admin@CM] /certificate> print detail
```

```
Flags: K - private-key, D - dsa, L - crl, C - smart-card-key,
```

```
A - authority, I - issued, R - revoked, E - expired, T - trusted
```

```
0 K   A T name="CAPsMAN-CA-000C424C30F3" common-name="CAPsMAN-CA-000C424C30F3" key-size=2048
          days-valid=24854 trusted=yes
```

```
          key-usage=digital-signature,key-encipherment,data-encipherment,key-cert-sign,crl-sign
          serial-number="1" fingerprint="69d77bbb45c50afd2d6c1785c2a3d72596b8a5f6"
          invalid-before=jan/01/1970 00:00:01 invalid-after=jan/18/2038 03:14:07
```

```
1 K   I   name="CAPsMAN-000C424C30F3" common-name="CAPsMAN-000C424C30F3" key-size=2048
          days-valid=24854 trusted=no key-usage=digital-signature,key-encipherment
          ca=CAPsMAN-CA-000C424C30F3 serial-number="1"
```

```
          fingerprint="e853ddb9d41fc139083a176ab164331bc24bc5ed"
          invalid-before=jan/01/1970 00:00:01 invalid-after=jan/18/2038 03:14:07
```

CAP can be configured to request certificate from CAPsMAN. In order for this to work, CAP must be configured with setting certificate=request and CAPsMAN must have CA certificate available (either specified in ca-certificate setting or auto-generated). 

CAP will initially generate private key and certificate request with CommonName of form "CAP-<mac address>". When CAP will establish connection with CAPsMAN, CAP will request CAPsMAN to sign its certificate request. If this will succeed, CAPsMAN will send CA certificate and newly issued certificate to CAP. CAP will import these certificates in its certificate store: 

```
[admin@CAP] > /interface wireless cap print
...
```

```
             requested-certificate: cert_2
       locked-caps-man-common-name: CAPsMAN-000C424C30F3
```

```
[admin@CAP] > /certificate print detail
Flags: K - private-key, D - dsa, L - crl, C - smart-card-key,
```

```
A - authority, I - issued, R - revoked, E - expired, T - trusted
```

```
0       T name="cert_1" issuer=CN=CAPsMAN-CA-000C424C30F3 common-name="CAPsMAN-CA-000C424C30F3"
          key-size=2048 days-valid=24837 trusted=yes
```

```
          key-usage=digital-signature,key-encipherment,data-encipherment,key-cert-sign,crl-sign
          serial-number="1" fingerprint="69d77bbb45c50afd2d6c1785c2a3d72596b8a5f6"
          invalid-before=jan/01/1970 00:00:01 invalid-after=jan/01/2038 03:14:07
```

```
1 K     T name="cert_2" issuer=CN=CAPsMAN-CA-000C424C30F3 common-name="CAP-000C4200C032"
          key-size=2048 days-valid=24837 trusted=yes
```

```
          key-usage=digital-signature,key-encipherment serial-number="2"
          fingerprint="2c85bf2fbc9fc0832e47cd2773a6f4b6af35ef65"
          invalid-before=jan/01/1970 00:00:01 invalid-after=jan/01/2038 03:14:07
```

On subsequent connections to CAPsMAN, CAP will use generated certificate.
