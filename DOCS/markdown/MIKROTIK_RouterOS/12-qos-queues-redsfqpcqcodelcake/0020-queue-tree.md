## `/queue tree` 

```
add name=download parent=Local packet-mark=PC1-traffic max-limit=10M bucket-size=10
add name=upload parent=Public packet-mark=PC1-traffic max-limit=10M bucket-size=10
```

Let's try to apply the same logic to a situation when bucket size is at its maximal value: 

In this case bucket-size=10, so bucket-capacity= 10 x 10M = 100M 

If the bucket is full (that is, the client was not using the full capacity of the queue for some time), the next 100Mb of traffic can pass through the queue at an unrestricted speed. 

So you can have: 

20Mbps transfer speed for 10s 

60Mbps transfer burst for 2s 

- 1Gbps transfer burst for approximately 100ms 

You can therefore see that the bucket permits a type of 'burstiness' of the traffic that passes through the queue. The behavior is similar to the normal burst feature but lacks the upper limit of the burst. This setback can be avoided if we utilize bucket size in the queue structure:
