## `/interface ethernet switch port` 

```
set ether1,ether2,ether3 pcp-based-qos-priority-mapping=0:0,1:1,2:2,3:3,4:4,5:5,6:6,7:7
```

Since the switch will empty the largest queue first and you need the highest priority to be served first, then you can assign this internal priority to a queue 1- to-1: 

606 

```
/interface ethernet switch port
```

```
set ether1,ether2,ether3 priority-to-queue=0:0,1:1,2:2,3:3,4:4,5:5,6:6,7:7
```

Finally, set each switch port to schedule packets based on the PCP value: 

```
/interface ethernet switch port
```

```
set ether1,ether2,ether3 qos-scheme-precedence=pcp-based
```
