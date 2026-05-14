## `/ip firewall mangle` 

```
add chain=forward action=mark-connection connection-mark=!heavy_traffic_conn new-connection-mark=all_conn
add chain=forward action=mark-connection connection-bytes=500000-0 connection-mark=all_conn connection-
rate=200k-100M new-connection-mark=heavy_traffic_conn protocol=tcp
```

```
add chain=forward action=mark-connection connection-bytes=500000-0 connection-mark=all_conn connection-
rate=200k-100M new-connection-mark=heavy_traffic_conn protocol=udp
```

```
add chain=forward action=mark-packet connection-mark=heavy_traffic_conn new-packet-mark=heavy_traffic
passthrough=no
```

```
add chain=forward action=mark-packet connection-mark=all_conn new-packet-mark=other_traffic passthrough=no
```
