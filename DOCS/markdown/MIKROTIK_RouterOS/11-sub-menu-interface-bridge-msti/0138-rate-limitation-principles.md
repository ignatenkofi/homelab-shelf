## Rate limitation principles 

Rate limiting is used to control the rate of traffic flow sent or received on a network interface. Traffic with rate that is less than or equal to the specified rate is sent, whereas traffic that exceeds the rate is dropped or delayed. 

Rate limiting can be performed in two ways: 

1.  discard all packets that exceed rate limit – rate-limiting (dropper or shaper) (100% rate limiter when queue-size=0) 

695 

2.  delay packets that exceed the specific rate limit in the queue and transmit them when it is possible – rate equalizing (scheduler) (100% rate equalizing when queue-size=unlimited) 

The next figure explains the difference between rate limiting and rate equalizing: 

**==> picture [504 x 249] intentionally omitted <==**

As you can see in the first case all traffic exceeds a specific rate and is dropped. In another case, traffic exceeds a specific rate and is delayed in the queue and transmitted later when it is possible, but note that the packet can be delayed only until the queue is not full. If there is no more space in the queue buffer, packets are dropped. 

For each queue we can define two rate limits: 

- CIR (Committed Information Rate) – ( limit-at in RouterOS) worst-case scenario, the flow will get this amount of traffic rate regardless of other traffic flows. At any given time, the bandwidth should not fall below this committed rate. 

- MIR (Maximum Information Rate) – ( max-limit in RouterOS) best-case scenario, the maximum available data rate for flow, if there is free any part of the bandwidth.
