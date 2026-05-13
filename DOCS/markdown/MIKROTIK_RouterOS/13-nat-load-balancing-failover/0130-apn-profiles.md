## APN profiles 

All network-related settings are under profiles 

```
Sub-menu: /interface lte apn
```

**==> picture [516 x 141] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>add-default-route  (yes |  Whether to add a default route to forward all traffic over the LTE interface.<br>no)<br>apn  (string) Service Provider's Access Point Name<br>authentication  (pap |  Allowed protocol to use for authentication<br>chap | none; Default:  none<br>)<br>default-route-distance  (in Sets distance value applied to auto-created default route, if add-default-route is also selected. LTE route by default is with<br>teger; Default: ) 2 distance 2 to prefer wired routes over LTE<br>**----- End of picture text -----**<br>


810 

**==> picture [516 x 314] intentionally omitted <==**

**----- Start of picture text -----**<br>
ip-type  (ipv4 | ipv4-ipv6 |  Requested PDN type<br>ipv6; Default: )<br>ipv6-interface  (; Default:  Interface on which to advertise IPv6 prefix<br>)<br>name  (string; Default: ) APN profile name<br>number  (integer;  APN profile number<br>Default: )<br>passthrough-interface  (;  Interface to passthrough IP configuration (activates passthrough)<br>Default: )<br>passthrough-mac  (MAC;  If set to auto, then will learn MAC from the first packet<br>Default:  auto )<br>passthrough-subnet- "auto" selects the smallest possible subnet to be used for the passthrough interface. "p2p" sets the passthrough interface<br>selection  (auto / p2p;  subnet as /32 and picks gateway address from 10.177.0.0/16 range. The gateway address stays the same until the apn<br>Default:  auto ) configuration is changed.<br>password  (string;  Password used if any of the authentication protocols are active<br>Default: )<br>use-network-apn  (yes |  Parameter is available starting from RouterOS v7 and used only for MBIM modems. If set to yes, uses network provided<br>no; Default:  yes ) APN.<br>use-peer-dns  (yes | no;  If set to yes, uses DNS received from LTE interface<br>Default:  yes )<br>user  (integer) Username used if any of the authentication protocols are active<br>**----- End of picture text -----**<br>
