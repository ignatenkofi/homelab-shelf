## Standards: `RFC 2136, RFC 3007` 

Dynamic DNS Update Tool gives a way to keep the domain name pointing to a dynamic IP address. It works by sending a domain name system update requests to the name server, which has a zone to be updated. Secure DNS updates are also supported. 

The DNS update tool supports only one algorithm - hmac-md5 . It's the only proposed algorithm for signing DNS messages. 

**==> picture [13 x 13] intentionally omitted <==**

DNS update tool works only with the BIND server, it will not work with DynDNS, EveryDNS, or any other similar service.
