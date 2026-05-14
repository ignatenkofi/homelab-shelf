## Interface 

Sub-menu: `/mpls ldp interface` 

**==> picture [516 x 240] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>afi ( ip | ipv6 ;  Default:  ) Determines interface address family. Only AFIs that are configured as supported by the instance is taken into account. If the<br>value is not explicitly specified then it is considered to be equal to the instance-supported AFIs.<br>accept-dynamic- Defines whether to discover neighbors dynamically or use only statically configured in LDP neighbors menu<br>neighbors  (yes | no;<br>Default:)<br>comments  (string;  Short description of the entry<br>Default: )<br>disabled  (yes | no;<br>Default: no )<br>hello-interval  (string;  The interval between hello packets that the router sends out on specified interface/s. The default value is 5s.<br>Default: )<br>hold-time  (string;  Specifies the interval after which a neighbor discovered on the interface is declared as not reachable. The default value is<br>Default: ) 15s.<br>interface  (string;  Name of the interface or interface list where LDP will be listening.<br>Default: )<br>**----- End of picture text -----**<br>

852 

transport-addresses (List Used transport addresses if differs from LDP Instance settings. of IPs; Default: )
