## Configuration Example 

Let's configure pppoe server compatible with Windows clients and MRRU enabled. 

```
[admin@RB800] /interface pppoe-server server> add service-name=myPPP interface=ether1 mrru=1614
```

```
[admin@RB800] /interface pppoe-server server> print
```

```
Flags: X - disabled
```

```
 0   service-name="myPPP" interface=ether1 max-mtu=1480 max-mru=1480 mrru=1614
     authentication=pap,chap,mschap1,mschap2 keepalive-timeout=10 one-session-per-host=no
     max-sessions=0 default-profile=default
```

In short - standard PPP link - just specify MRRU in both sides.
