## DNS over HTTPS (DoH) 

RouterOS support DNS over HTTPS (DoH). DoH uses HTTPS protocol to send and receive DNS requests for better data integrity. The main goal is to provide privacy by eliminating "man-in-the-middle" attacks (MITM). 

Video: DoH setup 

**==> picture [13 x 13] intentionally omitted <==**

It is strongly recommended to import the root CA certificate of the DoH server you have chosen to use for increased security. We strongly suggest not using third-party download links for certificate fetching. Use the Certificate Authority's own website. 

There are various ways to find out what root CA certificate is necessary. The easiest way is by using your WEB browser, navigating to the DoH site, and checking the security of the website. You can download the certificate straight from the browser or fetch the certificate from a trusted source. 

Download the certificate, upload it to your router and import it: 

```
/certificate import file-name=CertificateFileName
```

Configure the DoH server: 

```
/ip dns set use-doh-server=DoH_Server_Query_URL verify-doh-cert=yes
```

919 

**==> picture [13 x 13] intentionally omitted <==**

Only one DoH server is supported. 

Note that you need at least one regular DNS server configured for the router to resolve the DoH hostname itself. 

```
/ip dns set servers=1.1.1.1
```

If you do not have any dynamical or static DNS server configured, add a static DNS entry for the DoH server domain name like this: 

```
/ip dns static add address=IP_Address name=Domain_Name
```

**==> picture [13 x 13] intentionally omitted <==**

If DoH server is being used (DoH DNS name can be resolved) then it will be the only DNS service working at the time and standard DNS servers from IP/DNS servers list will not be used. 

**==> picture [13 x 13] intentionally omitted <==**

- If /certificate/settings/set crl-use is set to yes, RouterOS will check CRL for each certificate in a certificate chain, therefore, an entire certificate chain should be installed into a device - starting from Root CA, intermediate CA (if there are such), and certificate that is used for specific service. 

For example, Google DoH, Cloudflare, and OpenDNS full chain contain three certificates,  NextDNS has four certificates.
