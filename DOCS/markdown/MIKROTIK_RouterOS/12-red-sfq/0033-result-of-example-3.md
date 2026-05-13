## Result of Example 3 

Queue03 will receive 2Mbps Queue04 will receive 6Mbps Queue05 will receive 2Mbps Clarification: After satisfying all limit-at s HTB will give throughput to the queue with the highest priority. But in this case, inner queue Queue02 had l imit-at specified, by doing so, it reserved 8Mbps of throughput for queues Queue04 and Queue05 . Of these two Queue04 has the highest priority, which is why it gets additional throughput.
