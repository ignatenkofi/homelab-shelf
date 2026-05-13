## Connection establishment process 

**==> picture [504 x 104] intentionally omitted <==**

1. The host A who needs to initialize a connection sends out an SYN (Synchronize) packet with a proposed initial sequence number to the destination "host B"; 

2. When the host B receives an SYN message, it returns a packet with both SYN and ACK flags set in the TCP header (SYN-ACK); 3. When the host A receives the SYN-ACK, it sends back the ACK (Acknowledgment) packet; 4. Host B receives ACK and at this stage, the connection is ESTABLISHED; 

Connection-oriented protocol services are often sending acknowledgments (ACKs) after successful delivery. After the packet with data is transmitted, the sender waits for acknowledgment from the receiver. If time expires and the sender did not receive ACK, a packet is retransmitted.
