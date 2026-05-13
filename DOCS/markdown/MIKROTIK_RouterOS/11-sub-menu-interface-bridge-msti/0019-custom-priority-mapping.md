## Custom priority mapping 

Sometimes certain VLAN or WMM priorities need to be changed or cleared to a default value. We can use the `ingress-priority` matcher in IP mangle or bridge firewall/nat rules to filter only the needed priorities and change them to a different value using the `new-priority` action setting. For example, forwarded VLAN tagged packets over a bridge with a priority of 5, need to be changed to 0. 

```
/interface bridge filter
```

```
add action=set-priority chain=forward ingress-priority=5 new-priority=0
```
