## Notes 

The two default profiles cannot be removed: 

```
[admin@rb13] ppp profile> print
Flags: * - default
 0 * name="default" use-compression=no use-encryption=no only-one=no
     change-tcp-mss=yes
 1 * name="default-encryption" use-compression=default use-encryption=yes
     only-one=default change-tcp-mss=default
[admin@rb13] ppp profile>
```

incoming-filter and outgoing-filter arguments add dynamic jump rules to chain ppp, where the jump-target argument will be equal to incoming-filter or outgoi ng-filter argument in the profile. Therefore, chain ppp should be manually added before changing these arguments. 

only-one parameter is ignored if RADIUS authentication is used. 

```
PPP tunnels uses LCP protocol for MTU negotiation, it happens right when connection is established. Framed MTU
attribute is not supported, as it is sent only after authentication with Radius.
```
