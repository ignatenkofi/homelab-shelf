## RIP Configuration 

To start RIP, the instance should be configured. There you should select which routes will be redistributed by RIP and if it will redistribute the default route. 

```
/routing/rip/instance
```

```
add name=instance1 originate-default=never redistribute=connected,static
```

Then interface-template should be configured. There is no need to define networks in ROS version 7 as it was in version 6. 

```
/routing/rip/interface-template
add interfaces=ether1 instance=instance1
```

Now the basic configuration is completed on one router. RIP neighbor router should be configured in a similar way. 

In ROS v7 the neighbors will appear only when there are routes to be sent or/and to be received. 

Prefix lists from ROSv6 are deprecated, now all the filtering must be done by the routing filters. 

1080
