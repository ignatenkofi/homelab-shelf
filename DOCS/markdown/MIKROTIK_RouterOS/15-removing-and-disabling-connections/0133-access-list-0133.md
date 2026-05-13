## Access List 

```
/ip/proxy/access
```

An access list is configured like regular firewall rules. Rules are processed from the top to the bottom. The first matching rule specifies the decision of what to do with this connection. There is a total of 6 classifiers that specify matching constraints. If none of these classifiers is specified, the particular rule will match every connection. 

If a connection is matched by a rule, the action property of this rule specifies whether a connection will be allowed or not. If the particular connection does not match any rule, it will be allowed. 

**==> picture [501 x 267] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>action  (allow | deny; Default: allow ) Specifies whether to pass or deny matched packets<br>dst-address  (Ip4[-Ip4 | /0..32] | Ip6/0..128;  The destination address of the target server.<br>Default: )<br>dst-host  (string; Default: ) IP address or DNS name used to make a connection to the target server (this is the string user<br>wrote in a browser before specifying the port and path to a particular web page<br>dst-port  (integer[-integer[,integer[,...]]]: 0.. List or range of ports the packet is destined to<br>65535; Default: )<br>local-port  (integer: 0..65535; Default: ) Specifies the port of the web proxy via which the packet was received. This value should match one<br>of the ports the web proxy is listening on.<br>method  (any | connect | delete | get | head |  The HTTP method used in the request (see HTTP Methods section at the end of this document)<br>options | post | put | trace; Default: )<br>path  (string; Default: ) Name of the requested page within the target server (i.e. the name of a particular web page or<br>document without the name of the server it resides on)<br>redirect-to  (string; Default: ) In case of access is denied by this rule, the user shall be redirected to the URL specified here<br>src-address  (Ip4[-Ip4 | /0..32] | Ip6/0..128;  The source address of the connection originator.<br>Default: )<br>**----- End of picture text -----**<br>


Read-only properties: 

**==> picture [251 x 42] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>hits  (integer) Count of requests that were matched by this rule<br>**----- End of picture text -----**<br>


935 

Wildcard properties (dst-host and dst-path) match a complete string (i.e., they will not match "example.com" if they are set to "example"). Available wildcards are '*' (match any number of any characters) and '?' (match any one character). Regular expressions are also accepted here, but if the property should be treated as a regular expression, it should start with a colon (':'). 

Small hints in using regular expressions: 

- \\ symbol sequence is used to enter \ character in the console; 

- \. pattern means. only (in regular expressions single dot in a pattern means any symbol); 

- to show that no symbols are allowed before the given pattern, we use the ^ symbol at the beginning of the pattern; to specify that no symbols are allowed after the given pattern, we use the $ symbol at the end of the pattern; to enter [ or ] symbols, you should escape them with backslash "\."; 

It is strongly recommended to deny all IP addresses except those behind the router as the proxy still may be used to access your internal-use-only (intranet) web servers. Also, consult examples in Firewall Manual on how to protect your router.
