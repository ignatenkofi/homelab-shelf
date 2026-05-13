## Default Queue Bucket 

```
/queue tree
```

```
add name=download parent=Local packet-mark=PC1-traffic max-limit=10M
add name=upload parent=Public packet-mark=PC1-traffic max-limit=10M
```

In this case bucket-size=0.1, so bucket-capacity= 0.1 x 10M = 1M 

707 

If the bucket is full (that is, the client was not using the full capacity of the queue for some time), the next 1Mb of traffic can pass through the queue at an unrestricted speed.
