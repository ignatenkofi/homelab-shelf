## WireGuard interface configuration 

First of all, WireGuard interfaces must be configured on both sites to allow automatic private and public key generation. The command is the same for both routers: 

```
/interface/wireguard
add listen-port=13231 name=wireguard1
```

Now when printing the interface details, both private and public keys should be visible to allow an exchange. 

**==> picture [13 x 13] intentionally omitted <==**

Any private key will never be needed on the remote side device - hence the name private.
