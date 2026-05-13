## Parameters 

**==> picture [516 x 509] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>broadcast   (  Allow receiving broadcast (FF:FF:FF:FF:FF:FF) packets.<br>yes | no;<br>Default:  yes )<br>comment  (stri Descriptive comment for the controller.<br>ng; Default: )<br>copy-from  (str Copies an existing item. It takes default values of a new item's properties from another item. If you do not want to make an exact copy,<br>ing; Default: ) you can specify new values for some properties. When copying items that have names, you will usually have to give a new name to a<br>copy.<br>instance  (string ZeroTier instance name.<br>; Default:  zt1 )<br>ip-range  (IP;  IP range, for example, 172.16.16.1-172.16.16.254.<br>Default: )<br>ip6-6plane  (  An option gives every member a /80 within a /40 network but uses NDP emulation to route all IPs under that /80 to their owner. The  6pl<br>yes | no;  ane  mode is great for use cases like Docker since it allows every member to assign IPv6 addresses within its /80 that just work<br>Default:  no ) instantly and globally across the network.<br>ip6-rfc4193  (  The rfc4193 mode gives every member a /128 on a /88 network.<br>yes | no;<br>Default:  no )<br>ip6-range  (IPv6 IPv6 range, for example fd00:feed:feed:beef::-fd00:feed:feed:beef:ffff:ffff:ffff:ffff.<br>; Default: )<br>mtu  (integer;  Network MTU.<br>Default:  2800 )<br>multicast-limit  ( Maximum recipients for a multicast packet.<br>integer:<br>Default:  32 )<br>name  (string;  A short name for this controller.<br>Default: )<br>network  (string 16-digit network ID.<br>; Default)<br>private  ( yes |  Enables access control.<br>no; Default:  y<br>es )<br>routes  (IP@GW Push routes in the following format:<br>; Default: ) Routes ::= Route[,Routes]<br>  Route ::= Dst[@Gw]<br>**----- End of picture text -----**<br>


Configuration example 

1288 

In the following example, we will use RouterOS built-in ZeroTier controller to send our new network hosts appropriate certificates, credentials, and configuration information. The controller will operate from the "RouterOS Home" device and we will join in our network 3 units: mobile phone, laptop, RouterOS Office device, but theoretically, you can join up to 100 devices in one network. 

**==> picture [504 x 354] intentionally omitted <==**
