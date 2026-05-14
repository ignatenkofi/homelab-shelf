## IP Binding 

```
/ip/hotspot/ip-binding
```

IP-Binding HotSpot menu allows to the setup of static One-to-One NAT translations, allows to bypass specific HotSpot clients without any authentication, and also allows to block specific hosts and subnets from the HotSpot network 

**==> picture [502 x 204] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP Range; Default: "" ) The original IP address of the client<br>mac-address  (MAC; Default: "" ) MAC address of the client<br>server  (string | all; Default: "all" ) Name of the HotSpot server.<br>all  - will be applied to all hotspot servers<br>to-address  (IP; Default: "" ) New IP address of the client, translation occurs on the router (client does not know anything about the<br>translation)<br>type  (blocked | bypassed | regular;  Type of the IP-binding action<br>Default: "" )<br>regular  - performs One-to-One NAT according to the rule, translates the  address to to-address<br>bypassed  - performs the translation, but excludes client from login to the HotSpot<br>blocked  - translation is not performed and packets from a host are dropped<br>**----- End of picture text -----**<br>
