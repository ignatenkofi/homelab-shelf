## Connection termination 

**==> picture [504 x 103] intentionally omitted <==**

When the data transmission is complete and the host wants to terminate the connection, the termination process is initiated. Unlike TCP Connection establishment, which uses a three-way handshake, connection termination uses four-way massages. A connection is terminated when both sides have finished the shutdown procedure by sending a FIN (finish) and receiving an ACK (Acknowledgment). 

158 

1.  The host A, who needs to terminate the connection, sends a special message with the FIN flag, indicating that it has finished sending the data; 

2.  The host B, who receives the FIN segment, does not terminate the connection but enters into a "passive close" (CLOSE_WAIT) state and sends the ACK for the FIN back to the host A. If host B does not have any data to transmit to the host A it will also send the FIN message. Now the host B enters into LAST_ACK state. At this point host B will no longer accept data from host A, but can continue to transmit data to host A. 

3.  When the host A receives the last FIN from the host B, it enters into a (TIME_WAIT) state, and sends an ACK back to the host B; 4.  Host B gets the ACK from the host A and connection is terminated;
