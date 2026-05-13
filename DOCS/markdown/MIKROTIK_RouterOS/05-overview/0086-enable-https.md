## Enable HTTPS 

For HTTPS to work properly, you need to specify a valid certificate that WebFig can use. You can use a certificate that is issued by a trusted Certificate Authority (CA) or you can create your own root CA and generate self-signed certificates. 

**==> picture [13 x 13] intentionally omitted <==**

WebFig supports wildcard certificates. You can generate such a certificate by specifying a wildcard in the common-name property, for example, common-name=*.mikrotik.com. 

To generate your own certificates and enable HTTPS access, you must configure the following: 

Create your own root CA on your router and sign it 

```
[admin@MikroTik] > certificate add name=local-cert common-name=local-cert key-usage=key-cert-sign,crl-sign
[admin@MikroTik] > certificate sign local-cert
  progress: done
```

**==> picture [13 x 13] intentionally omitted <==**

In case you already have set up your own CA or you are using a service that signs certificates for you, then you need to create and sign the certificate remotely and import the certificate on the router later. In case you are importing a certificate, then make sure you mark the certificate as trusted. 

Create a new certificate for WebFig (non-root certificate) 

252 

```
[admin@MikroTik] > certificate add name=webfig common-name=192.168.88.1
[admin@MikroTik] > certificate sign webfig
  progress: done
[admin@MikroTik] > certificate print
Flags: K - private-key; A - authority; T - trusted
Columns:NAME        COMMON-NAME     FINGERPRINT
0  KAT  local-cert  local-cert      9b6363d033c4b2e6893c340675cfb8d1e330977526dba347a440fabffd983c5d
1  KAT  webfig      192.168.88.1    9f84ac2979bea65dccd02652056e5559bcdf866f8da5f924139d99453402bd02
```

Enable www-ssl and specify to use the newly created certificate for WebFig 

```
[admin@MikroTik] > ip service
set www-ssl certificate=webfig disabled=no
```

You can now visit https://192.168.88.1 and securely configure your router. 

**==> picture [13 x 13] intentionally omitted <==**

By default, browsers will not trust self-signed certificates, you will need to add the certificate as trusted on the first time you visit the page in your browser. Another approach is to export the root CA certificate and import it as a trusted root certificate on your computer, this way all certificates signed by this router will be considered as valid and will make it easier to manage certificates in your network. 

**==> picture [13 x 13] intentionally omitted <==**

Most Internet browsers have their own certificate trust chain and work independently of the operating system's certificate trust chain, this means that you may have to add your own root CA's certificate as a trusted certificate in your browser settings since trusting the certificate in your operating system's settings might not have any effect when using your Internet browser.
