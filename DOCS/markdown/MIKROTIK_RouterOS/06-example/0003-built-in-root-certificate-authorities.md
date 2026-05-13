## Built-in root certificate authorities 

Starting from RouterOS 7.19, RouterOS contains list of built-in root certificate authorities that can be used for host certificate verification. 

Now it is possible to use DoH, download Adlist from URL or use fetch tool with certificate validation without the need to manually import the relevant root certificate. 

The list of built-in root certificate authorities is accessible in System → Certificates → Built In CA 

**==> picture [13 x 13] intentionally omitted <==**

When upgrading from older RouterOS version, by default built-in root certificates are not trusted. 

Execute /certificate/settings/set builtin-trust-anchors=trusted to change trust settings for these certificates 

283
