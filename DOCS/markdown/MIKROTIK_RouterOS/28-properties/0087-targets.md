## Targets 

Sub-menu: `/ip traffic-flow target` 

With Traffic-Flow targets we specify those hosts which will gather the Traffic-Flow information from the router. 

**==> picture [516 x 147] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>src-address  (IP ; Default: ) IP address used as source when sending Traffic-Flow statistics<br>dst- address  (IP; Default: ) IP address of the host which receives Traffic-Flow statistic packets from the router.<br>Port  (Port; Default:2055) Port (UDP) of the host which receives Traffic-Flow statistic packets from the router.<br>v9-template-refresh  (integer; Default:  20 ) Number of packets after which the template is sent to the receiving host (only for NetFlow version 9 and<br>IPFIX)<br>v9-template-timeout  (time; Default: ) After how long to send the template, if it has not been sent. (only for NetFlow version 9 and IPFIX)<br>version  (1 | 5 | 9 | IPFIX; Default: ) Which version format of NetFlow to use<br>**----- End of picture text -----**<br>
