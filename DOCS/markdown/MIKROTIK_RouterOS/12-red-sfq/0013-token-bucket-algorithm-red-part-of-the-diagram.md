## Token Bucket algorithm (Red part of the diagram) 

The Token Bucket algorithm is based on an analogy to a bucket where tokens, represented in bytes, are added at a specific rate. The bucket itself has a specified capacity. 

If the bucket fills to capacity, newly arriving tokens are dropped. 

Bucket capacity = bucket-size * max-limit 

bucket size (0..10, Default:0.1) 

Before allowing any packet to pass through the queue, the queue bucket is inspected to see if it already contains sufficient tokens at that moment. 

If yes, the appropriate number of tokens are removed ("cashed in") and the packet is permitted to pass through the queue. 

If not, the packets stay at the start of the packet waiting queue until the appropriate amount of tokens is available. 

In the case of a multi-level queue structure, tokens used in a child queue are also 'charged' to their parent queues. In other words - child queues 'borrow' tokens from their parent queues.
