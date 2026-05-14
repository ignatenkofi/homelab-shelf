## Priority 

We already know that limit-at ( CIR ) to all queues will be given out no matter what. 

Priority is responsible for the distribution of remaining parent queues traffic to child queues so that they are able to reach max-limit 

The queue with higher priority will reach its max-limit before the queue with lower priority. 8 is the lowest priority, and 1 is the highest. 

Make a note that priority only works: 

for leaf queues - priority in the inner queue has no meaning. if max-limit is specified (not 0)
