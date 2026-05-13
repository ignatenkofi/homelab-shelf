## Explanation 

In mangle, we need to separate all connections into two groups, and then mark packets from their 2 groups. As we are talking about client traffic most logical place for marking would be the mangle chain forward. 

Keep in mind that as soon as a "heavy" connection will have lower priority and queue will hit max-limit - heavy connection will drop speed, and connectionrate will be lower. This will result in a change to a higher priority and the connection will be able to get more traffic for a short while, when again connectionrate will rise and that again will result in a change to lower priority). To avoid this we must make sure that once detected "heavy connections" will remain marked as "heavy connections" for all times.
