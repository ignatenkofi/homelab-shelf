## Application Example - Traffic Prioritization 

Connection-rate can be used in various ways, that still need to be realized, but the most common setup will be to detect and set lower priorities to the "heavy connections" (connections that maintain a fast rate for long periods (such as P2P, HTTP, FTP downloads). By doing this you can prioritize all other traffic that usually includes VoIP and HTTP browsing and online gaming. 

The method described in this example can be used together with other ways to detect and prioritize traffic. As the connection-rate option does not have any averages we need to determine what will be the margin that identifies "heavy connections". If we assume that a normal HTTP browsing connection is less than 500kB (4Mb) long and VoIP requires no more than 200kbps speed, then every connection that after the first 500kB still has more than 200kbps speed can be assumed as "heavy". 

(You might have different "connection-bytes" for HTTP browsing and different "connection-rate" for VoIP in your network - so, please, do your own research before applying this example) 

For this example, let's assume that we have a 6Mbps upload and download connection to ISP. 

744
