## PPPoE Client 

1254 

To configure MikroTik RouterOS to be a PPPoE client, just add a PPPoE-client with the following parameters as in the example: 

```
[admin@MikroTik] > interface pppoe-client add interface=ether2 password=StrongPass service-name=pppoeservice
name=PPPoE-Out disabled=no user=MT-User
```

```
[admin@MikroTik] > interface pppoe-client print
Flags: X - disabled, I - invalid, R - running
```

```
 0  R name="PPPoE-Out" max-mtu=auto max-mru=auto mrru=disabled interface=ether2 user="MT-User"
      password="StrongPass" profile=default keepalive-timeout=10 service-name="pppoeservice" ac-name=""
      add-default-route=no dial-on-demand=no use-peer-dns=no allow=pap,chap,mschap1,mschap2
```
