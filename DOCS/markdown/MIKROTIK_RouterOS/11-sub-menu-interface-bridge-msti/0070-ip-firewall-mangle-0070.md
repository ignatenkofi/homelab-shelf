## `/ip firewall mangle` 

```
add chain=forward in-interface=local src-address=192.168.88.123 connection-state=new action=mark-connection new-
connection-mark=client_conn
```

```
add chain=forward connection-mark=client_conn action=mark-packet new-packet-mark=client_p
```

**==> picture [13 x 13] intentionally omitted <==**

Warning: Packet marks are limited to a maximum of 4096 unique entries. Exceeding this limit will cause an error "bad new packet mark"
