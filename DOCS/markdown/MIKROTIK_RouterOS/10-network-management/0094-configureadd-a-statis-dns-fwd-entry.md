## Configure/add a statis DNS FWD entry: 

```
/ip dns static
add forward-to=forwarder1 name=mikrotik.com type=FWD
```

Now each time when a router will receive request to resolve mikrotik.com, request using round-robin algorithm will be forwarded to 1.1.1.1, local.dns or Goo gle DoH server. 

922
