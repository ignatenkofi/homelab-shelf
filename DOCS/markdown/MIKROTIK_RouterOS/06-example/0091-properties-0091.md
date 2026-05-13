## Properties 

**==> picture [516 x 351] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>accounting-backup  (yes | no; Default:  no ) Whether the configuration is for the backup RADIUS server<br>accounting-port  (integer [1..65535]; Default:  1813 ) RADIUS server port used for accounting<br>address  (IPv4/IPv6 address; Default:  0.0.0.0 ) IPv4 or IPv6 address of RADIUS server.<br>The following formats are accepted:<br>- ipv4<br>- ipv4 @ vrf<br>- ipv6<br>- ipv6 @ vrf<br>authentication-port  (integer [1..65535]; Default:  1812 ) RADIUS server port used for authentication.<br>called-id  (string; Default: ) Value depends on Point-to-Point protocol: PPPoE - service name, PPTP - server's IP<br>address, L2TP - server's IP address.<br>certificate  (string; Default: ) Certificate file to use for communicating with RADIUS Server with RadSec enabled.<br>comment  (string; Default: )<br>disabled  (yes | no; Default:  no )<br>domain  (string; Default: ) Microsoft Windows domain of client passed to RADIUS servers that require domain<br>validation.<br>protocol  (radsec | udp; Default:  udp ) Specifies the protocol to use when communicating with the RADIUS Server.<br>radsec-timeout  (time, Default:  3300ms ) Timeout after which the request should be resent over RadSec protocol.<br>require-message-auth  (no | yes-for-request-resp Default:  y Specifies if Message-Authenticator attributes are required.<br>es-for-request-resp )<br>**----- End of picture text -----**<br>


314 

**==> picture [516 x 207] intentionally omitted <==**

**----- Start of picture text -----**<br>
realm  (string; Default: ) Explicitly stated realm (user domain), so the users do not have to provide proper ISP<br>domain name in the user name.<br>secret  (string; Default: ) The shared secret used to access the RADIUS server.<br>service  (ppp|login|hotspot|wireless|dhcp|ipsec|dot1x;  Router services that will use this RADIUS server:<br>Default: )<br>hotspot - HotSpot authentication service<br>login - router's local user authentication<br>ppp - Point-to-Point clients authentication<br>wireless - wireless client authentication<br>dhcp - DHCP protocol client authentication (client's MAC address is sent as User-<br>Name)<br>ipsec - ipsec client authentification<br>dot1x - dot1x authentification<br>src-address  (ipv4/ipv6 address; Default:  0.0.0.0 ) Source IP/IPv6 address of the packets sent to the RADIUS server<br>timeout  (time; Default:  1100ms ) Timeout after which the request should be resent.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

When the RADIUS server is authenticating the user with CHAP, MS-CHAPv1, MS-CHAPv2, it is not using a shared secret, the secret is used only in the authentication reply, and the router (RADIUS client) verifies it. So if you have the wrong shared secret, the RADIUS server will accept a request, but the router won't accept the reply. You can see that with "/radius monitor" command, the "bad-replies" number should increase whenever somebody tries to connect. 

**==> picture [13 x 13] intentionally omitted <==**

If RadSec is enabled, make sure your RADIUS Server is using " radsec " as the shared secret, otherwise, the RADIUS Server will not be able to decrypt data correctly (unprintable characters). With RadSec RouterOS forces the shared secret to "radsec" regardless of what has been set manually. For more details see - RFC6614.
