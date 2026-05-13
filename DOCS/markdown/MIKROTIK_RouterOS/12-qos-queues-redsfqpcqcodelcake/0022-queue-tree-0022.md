## `/queue tree` 

```
add name=download_parent parent=Local max-limit=20M
```

```
add name=download parent=download_parent packet-mark=PC1-traffic max-limit=10M bucket-size=10
add name=upload_parent parent=Public max-limit=20M
```

```
add name=upload parent=upload_parent packet-mark=PC1-traffic max-limit=10M bucket-size=10
```

In this case: 

parent queue bucket-size=0.1, bucket-capacity= 0.1 x 20M = 2M 

child queue bucket-size=10, bucket-capacity= 10 x 10M = 100M 

The parent will run out of tokens much faster than the child queue and as its child queue always borrows tokens from the parent queue the whole system is restricted to token-rate of the parent queue - in this case to max-limit=20M. This rate will be sustained until the child queue runs out of tokens and will be restricted to its token rate of 10Mbps. 

In this way, we can have a burst at 20Mbps for up to 10 seconds.
