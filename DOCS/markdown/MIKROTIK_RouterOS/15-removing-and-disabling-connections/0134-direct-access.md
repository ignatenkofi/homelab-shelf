## Direct Access 

```
/ip/proxy/direct
```

If a parent-proxy property is specified, it is possible to tell the proxy server whether to try to pass the request to the parent proxy or to resolve it by connecting to the requested server directly. The direct Access List is managed just like the Proxy Access List described in the previous chapter except for the action argument. Unlike the access list, the direct proxy access list has a default action equal to deny. It takes place when no rules are specified or a particular request did not match any rule. 

**==> picture [501 x 297] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (allow | deny; Default: allow ) Specifies the action to perform on matched packets:<br>allow - always resolve matched requests directly bypassing the parent router<br>deny - resolve matched requests through the parent proxy. If no one is specified this has the<br>same effect as allow .<br>dst-address  (Ip4[-Ip4 | /0..32] | Ip6/0..128;  The destination address of the target server.<br>Default: )<br>dst-host  (string; Default: ) IP address or DNS name used to make a connection to the target server (this is the string user<br>wrote in a browser before specifying port and path to a particular web page<br>dst-port  (integer[-integer[,integer[,...]]]: 0.. List or range of ports used by connection to the target server.<br>65535; Default: )<br>local-port  (integer: 0..65535; Default: ) Specifies the port of the web proxy via which the packet was received. This value should match<br>one of the ports the web proxy is listening on.<br>method  (any | connect | delete | get | head |  The HTTP method used in the request (see HTTP Methods section at the end of this document)<br>options | post | put | trace; Default: )<br>path  (string; Default: ) Name of the requested page within the target server (i.e. the name of a particular web page or<br>document without the name of the server it resides on)<br>src-address  (Ip4[-Ip4 | /0..32] | Ip6/0..128;  The source address of the connection originator.<br>Default: )<br>**----- End of picture text -----**<br>


Read-only properties: 

**==> picture [251 x 42] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>hits  (integer) Count of requests that were matched by this rule<br>**----- End of picture text -----**<br>


936 

Cache Management
