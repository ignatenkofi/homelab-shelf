## `/ip firewall nat` 

```
add action=endpoint-independent-nat chain=dstnat in-interface=WAN protocol=udp
```

**==> picture [13 x 13] intentionally omitted <==**

Endpoint-independent NAT works only with UDP protocol. 

Additionally, endpoint-independent-nat can take a few other parameters: 

**`randomize-port`** - randomize to which public port connections will be mapped. 

More info https://www.ietf.org/rfc/rfc5128.txt section 2.2.3 and 2.2.5 

653
