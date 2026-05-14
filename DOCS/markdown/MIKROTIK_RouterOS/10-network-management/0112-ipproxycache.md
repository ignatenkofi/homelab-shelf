## `/ip/proxy/cache` 

The cache access list specifies, which requests (domains, servers, pages) have to be cached locally by web proxy, and which do not. This list is implemented exactly the same way as the web proxy access list. The default action is to cache an object (if no matching rule is found). 

**==> picture [501 x 286] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (allow | deny; Default: allow ) Specifies the action to perform on matched packets:<br>allow - cache objects from matched request<br>deny - do not cache objects from matched request<br>dst-address  (Ip4[-Ip4 | /0..32] | Ip6/0..128;  The destination address of the target server<br>Default: )<br>dst-host  (string; Default: ) IP address or DNS name used to make a connection to the target server (this is the string user<br>wrote in a browser before specifying port and path to a particular web page<br>dst-port  (integer[-integer[,integer[,...]]]: 0.. List or range of ports the packet is destined to.<br>65535; Default: )<br>local-port  (integer: 0..65535; Default: ) Specifies the port of the web proxy via which the packet was received. This value should match<br>one of the ports the web proxy is listening on.<br>method  (any | connect | delete | get | head |  The HTTP method used in the request (see HTTP Methods section at the end of this document)<br>options | post | put | trace; Default: )<br>path  (string; Default: ) Name of the requested page within the target server (i.e. the name of a particular web page or<br>document without the name of the server it resides on)<br>src-address  (Ip4[-Ip4 | /0..32] | Ip6/0..128;  The source address of the connection originator<br>Default: )<br>**----- End of picture text -----**<br>

Read-only properties: 

**==> picture [251 x 42] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>hits  (integer) Count of requests that were matched by this rule<br>**----- End of picture text -----**<br>
