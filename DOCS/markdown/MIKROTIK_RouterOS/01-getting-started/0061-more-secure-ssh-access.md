## More Secure SSH access 

It is possible to enable more strict SSH settings (add aes-128-ctr and disallow hmac sha1 and groups with sha1) with this command: 

```
/ip ssh set strong-crypto=yes
```
