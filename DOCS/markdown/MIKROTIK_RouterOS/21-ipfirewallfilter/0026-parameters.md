## Parameters 

```
[admin@MikroTik] > zerotier/
```

**==> picture [516 x 371] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string; default:  zt1 ) Instance name.<br>port  (number; default:  9993 ) Port number the instance listen to.<br>identity  (string; default) Instance 40-bit unique address.<br>interface  (string; default:  all) List of interfaces that are used in order to discover ZeroTier peers, by using ARP and IP type connections.<br>route-distance  (number; default:  ) 1 Route distance for routes obtained from planet/moon servers.<br>[admin@MikroTik] > zerotier/interface/<br>Property Description<br>allow-default  (string; yes | no) A network can override the systems default route (force VPN mode).<br>allow-global  (string; yes | no) ZeroTier IP addresses and routes can overlap public IP space.<br>allow-managed  (string; yes | no) ZeroTier managed IP addresses and routes are assigned.<br>arp-timeout  ( number; default:  auto ) ARP timeouts value.<br>comment  (string; Default: ) Descriptive comment for the interfaces.<br>copy-from  Allows copying existing interfaces configuration.<br>disable-running-check  (string; yes | no) Force interface in "running" state.<br>instance  (string; Default: zt1 ) ZeroTier instance name.<br>name  (string; default:  zerotier1 ) A short name.<br>network  (string; Default) 16-digit network ID.<br>**----- End of picture text -----**<br>
