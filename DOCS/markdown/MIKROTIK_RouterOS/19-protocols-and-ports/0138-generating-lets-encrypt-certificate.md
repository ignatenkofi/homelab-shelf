## Generating Let's Encrypt certificate 

During the EAP-MSCHAPv2 authentication, TLS handshake has to take place, which means the server has to have a certificate that can be validated by the client. To simplify this step, we will use Let's Encrypt certificate which can be validated by most operating systems without any intervention by the user. To generate the certificate, simply enable SSL certificate under the Certificates menu. By default the command uses the dynamic DNS record provided by IP Cloud, however a custom DNS name can also be specified. Note that, the DNS record should point to the router. 

```
/certificate enable-ssl-certificate
```

If the certificate generation succeeded, you should see the Let's Encrypt certificate installed under the Certificates menu. 

```
/certificate print detail where name~"letsencrypt"
```
