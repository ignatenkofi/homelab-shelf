## `/radius` 

```
add address=10.1.2.3 secret=radiussecret service=dot1x
```

**==> picture [13 x 13] intentionally omitted <==**

If RADIUS communication is done over public network, it is advised to use RadSec for RADIUS communication. More information: RADIUS 

Add new dot1x server instances. 

```
/interface dot1x server
add interface=ether2 interim-update=30s comment=accounted
add interface=ether12 accounting=no comment=notaccounted
```
