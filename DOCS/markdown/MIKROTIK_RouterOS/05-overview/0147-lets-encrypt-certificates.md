## Let's Encrypt certificates 

RouterOS v7 has Let's Encrypt (letsencrypt) certificate support for the 'www-ssl' service. To enable the Let's Encrypt certificate service with automatic certificate renewal, use the 'enable-ssl-certificate' command: 

```
/certificate enable-ssl-certificate dns-name=my.domain.com
```

Note that the DNS name must point to the router. If the dns-name is not specified, it will default to the automatically generated /ip cloud name (ie. http://exa mple.sn.mynetname.net) 

If the used DNS name is not the default http://example.sn.mynetname.net, port TCP/80 must be available from the WAN. 

The certificate is automatically renewed when 80% of its validity period had passed.
