## Result of Example 4 

Queue03 will receive ~3Mbps Queue04 will receive ~1Mbps Queue05 will receive ~6Mbps 

Clarification: Only by satisfying all limit-at s HTB was forced to allocate 20Mbps - 6Mbps to Queue03 , 2Mbps to Queue04 , and 12Mbps to Queue05 , but our output interface is able to handle 10Mbps. As the output interface queue is usually FIFO throughput allocation will keep the ratio 6:2:12 or 3:1:6 

713
