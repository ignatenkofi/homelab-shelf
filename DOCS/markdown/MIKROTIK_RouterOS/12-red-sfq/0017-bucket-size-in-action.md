## Bucket Size in action 

Let's have a simple setup where all traffic from and to one IP address is marked with a packet-mark: 

```
/ip firewall mangle
```

```
add chain=forward action=mark-connection connection-mark=no-mark src-address=192.168.88.101 new-connection-
mark=pc1_conn
```

```
add chain=forward action=mark-connection connection-mark=no-mark dst-address=192.168.88.101 new-connection-
mark=pc1_conn
```

```
add chain=forward action=mark-packet connection-mark=pc1_conn new-packet-mark=pc1_traffic
```
