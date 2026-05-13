## Testing status 

On server side check if dynamic DHCP server is added and prefix is bound to specific client: 

1256 

```
[admin@RB1100] /ipv6 dhcp-server> print
Flags: D - dynamic, X - disabled, I - invalid
 #    NAME              INTERFACE            ADDRESS-POOL            LEASE-TIME
 0 D  <pppoe-a1>        <pppoe-a1>           myPool                  3d
[admin@RB1100] /ipv6 dhcp-server binding> print
Flags: X - disabled, D - dynamic
 #   ADDRESS                                        DU       IAID SER.. STATUS
 1 D 2001:db8:7501:ff04::/62                                  247 <pp.. bound
```

On client side, check if DHCP client is bound and pool is added: 

```
[admin@x86-test] /ipv6 dhcp-client> print
Flags: D - dynamic, X - disabled, I - invalid
 #    INTERFACE           STATUS        PREFIX                            EXPIRES-AFTER
0    client-test          bound         2001:db8:7501:ff04::/62           2d23h18m17s
[admin@x86-test] /ipv6 pool> print
Flags: D - dynamic
 #   NAME                        PREFIX                                   PREFIX-LENGTH
 0 D ppp-test                    2001:db8:7501:ff04::/62                             64
```

1257
