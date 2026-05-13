## `/ip firewall mangle` 

```
add chain=forward action=mark-connection connection-mark=!heavy_traffic_conn new-connection-mark=all_conn
```

These two rules will mark all heavy connections based on our standards, that every connection that after the first 500kB still has more than 200kbps speed can be assumed as "heavy": 

```
add chain=forward action=mark-connection connection-bytes=500000-0 \
```

```
    connection-mark=all_conn connection-rate=200k-100M new-connection-mark=heavy_traffic_conn protocol=tcp
add chain=forward action=mark-connection connection-bytes=500000-0 \
```

```
    connection-mark=all_conn connection-rate=200k-100M new-connection-mark=heavy_traffic_conn protocol=udp
```
