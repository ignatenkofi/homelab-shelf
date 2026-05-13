## Examples 

This example shows how to configure Traffic-Flow on a router 

Enable Traffic-Flow on the router: 

1824 

```
[admin@MikroTik] ip traffic-flow> set enabled=yes
[admin@MikroTik] ip traffic-flow> print
                enabled: yes
             interfaces: all
          cache-entries: 1k
    active-flow-timeout: 30m
  inactive-flow-timeout: 15s
[admin@MikroTik] ip traffic-flow>
```
