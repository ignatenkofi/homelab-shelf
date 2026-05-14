## `/ip ipsec mode-conf` 

```
set [find name="rw-conf"] system-dns=no static-dns=10.5.8.1
```

While it is possible to adjust the IPsec policy template to only allow road warrior clients to generate policies to network configured by split-include parameter , this can cause compatibility issues with different vendor implementations (see known limitations). Instead of adjusting the policy template, allow access to a secured network in IP/Firewall/Filter and drop everything else.
