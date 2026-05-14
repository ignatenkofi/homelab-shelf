## TCP Segments transmission (windowing) 

Now that we know how the TCP connection is established we need to understand how data transmission is managed and maintained. In TCP/IP networks transmission between hosts is handled by TCP protocol. 

Let’s think about what happens when data-grams are sent out faster than the receiving device can process. The receiver stores them in memory called a buffer. But since buffer space is not unlimited, when its capacity is exceeded receiver starts to drop the frames. All dropped frames must be retransmitted again which is the reason for low transmission performance. 

To address this problem, TCP uses a flow control protocol. The window mechanism is used to control the flow of the data. When a connection is established, the receiver specifies the window field in each TCP frame. Window size represents the amount of received data that the receiver is willing to store in the buffer. Window size (in bytes) is sent together with acknowledgments to the sender. So the size of the window controls how much information can be transmitted from one host to another without receiving an acknowledgment. The sender will send only the amount of bytes specified in window size and then will wait for acknowledgments with updated window size. 

If the receiving application can process data as quickly as it arrives from the sender, then the receiver will send a positive window advertisement (increase the size of the window) with each acknowledgment. It works until the sender becomes faster than the receiver and incoming data will eventually fill the receiver's buffer, causing the receiver to advertise acknowledgment with a zero window. A sender that receives a zero window advertisement must stop transmit until it receives a positive window.  Let's take a look at the illustrated windowing process: 

**==> picture [504 x 285] intentionally omitted <==**

1.  The "host A" starts to transmit with a window size of 1000, one 1000byte frame is transmitted; 

2.  Receiver "host B" returns ACK with window size to increase to 2000; 

159 

3.  The host A receives ACK and transmits two frames (1000 bytes each); 

4.  After that, the receiver advertises an initial window size to 3000. Now sender transmits three frames and waits for an acknowledgement; 

5.  The first three segments fill the receiver's buffer faster than the receiving application can process the data, so the advertised window size reaches zero indicating that it is necessary to wait before further transmission is possible; 

6.  The size of the window and how fast to increase or decrease the window size is available in various TCP congestion avoidance algorithms such as Reno, Vegas, Tahoe, etc; 

160
