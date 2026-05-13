## Basic Configuration Example 

Basic IS-IS setup between three routers. 

R1: 

1019 

```
/routing isis instance
```

```
add afi=ip areas=49.2222 disabled=no name=isis-instance-1 system-id=90ab.cdef.0001
/routing isis interface-template
```

```
add instance=isis-instance-1 interfaces=ether1 levels=l1,l2
```

```
[] /routing/isis/neighbor> print
```

```
 0 instance=isis-instance-1 interface=ether1 level-type=l2 snpa=08:00:27:22:B4:A2 srcid="1111.2222.aded"
state=up
```

```
 1 instance=isis-instance-1 interface=ether1 level-type=l2 snpa=D4:CA:6D:78:2F:2E srcid="1111.2222.cded"
state=up
```

```
 2 instance=isis-instance-1 interface=ether1 level-type=l1 snpa=08:00:27:22:B4:A2 srcid="1111.2222.aded"
state=up
```

```
 3 instance=isis-instance-1 interface=ether1 level-type=l1 snpa=D4:CA:6D:78:2F:2E srcid="1111.2222.cded"
state=up
```

```
[] /routing/route> print where is-is
Flags: A - ACTIVE; i - IS-IS
Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE, IMMEDIATE-GW
   DST-ADDRESS        GATEWAY                AFI  DISTANCE  SCOPE  TARGET-SCOPE  IMMEDIATE-GW
 i 0.0.0.0/0          10.155.101.214%ether1  ip4       115     20            10  10.155.101.214%ether1
 i 10.155.101.0/24    10.155.101.216%ether1  ip4       115     20            10  10.155.101.216%ether1
Ai 10.255.255.162/32  10.155.101.216%ether1  ip4       115     20            10  10.155.101.216%ether1
```
