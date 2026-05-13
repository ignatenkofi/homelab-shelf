## Properties 

**==> picture [516 x 256] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>auth  (md5  sha1  null  sha256  sha512| | | | ; Default:  sh Authentication methods that the server will accept.<br>a1,md5,sha256,sha512 )<br>certificate  (name  none| ; Default:  none ) Name of the certificate that the OVPN server will use.<br>cipher  (null | aes128-cbc | aes128-gcm | aes192-cbc Allowed ciphers.<br>| aes192-gcm | aes256-cbc | aes256-gcm | blowfish1<br>28; Default:  aes128-cbc,blowfish128 )<br>default-profile  (name; Default:  default ) Default profile to use.<br>disabled  (yes  no| ; Default:  yes ) Defines whether the OVPN server is enabled or not.<br>protocol (tcp  udp| ; Default: tcp) Indicates the protocol to use when connecting with the remote endpoint.<br>keepalive-timeout  (integer  disabled| ; Default:  60 ) Defines the time period (in seconds) after which the router is starting to send keepalive packets<br>every second. If no traffic and no keepalive responses have come for that period of time (i.e. 2 *<br>keepalive-timeout), not responding client is proclaimed disconnected<br>mac-address  (MAC; Default: ) Automatically generated MAC address of the server.<br>max-mtu  (integer; Default:  1500 ) Maximum Transmission Unit. Max packet size that the OVPN interface will be able to send<br>without packet fragmentation.<br>**----- End of picture text -----**<br>


1246 

**==> picture [516 x 390] intentionally omitted <==**

**----- Start of picture text -----**<br>
mode  (ip  ethernet| ; Default: ) ip Layer3 or layer2 tunnel mode (alternatively tun, tap)<br>name  (string) Name of the server<br>netmask  (integer; Default:  24 ) Subnet mask to be applied to the client.<br>port  (integer; Default:  1194 ) Port to run the server on.<br>require-client-certificate  (yes  no| ; Default:  no ) If set to yes, then the server checks whether the client's certificate belongs to the same<br>certificate chain.<br>redirect-gateway  (def1  disabled  ipv6;| |  Default:  disa Specifies what kind of routes the OVPN client must add to the routing table.<br>bled )<br>def1  – Use this flag to override the default gateway by using 0.0.0.0/1 and 128.0.0.0/1 rather<br>than 0.0.0.0/0. This has the benefit of overriding but not wiping out the original default gateway.<br>disabled  - Do not send redirect-gateway flags to the OVPN client.<br>ipv6  - Redirect IPv6 routing into the tunnel on the client side. This works similarly to the def1<br>flag, that is, more specific IPv6 routes are added (2000::/4 and 3000::/4), covering the whole<br>IPv6 unicast space.<br>enable-tun-ipv6  (yes  no;|  Default:  no ) Specifies if IPv6 IP tunneling mode should be possible with this OVPN server.<br>ipv6-prefix-len  (integer; Default:  64 ) Length of IPv6 prefix for IPv6 address which will be used when generating OVPN interface on<br>the server side.<br>reneg-sec   (integer; Default:  3600) Key renegotiate seconds, the time the server periodically renegotiates the secret key for the data<br>channel.<br>push-routes  (string; Default: ) Push route support are added in 7.14, the maximum of possible input is limited to 1400<br>characters. IPv6 support added in 7.21_ab220.<br>tls-version  (any | only-1.2 ; Default:  any  ) TLS protocol setting.<br>tun-server-ipv6  (IPv6 prefix; Default: ) :: IPv6 prefix address which will be used when generating the OVPN interface on the server side.<br>user-auth-method  (mschap2 | pap ; Default  pap ) By the default pap authentication method is used, if preferred server authentication with chap<br>challenge set mschap2 in server settings.<br>vrf  () VRF in which listen for connection attempts<br>**----- End of picture text -----**<br>


Also, it is possible to prepare a .ovpn file for the OVPN client which can be easily imported on the end device. Server need to have option enabled - required client certificate to export work. 

```
interface/ovpn-server/server/export-client-configuration ca-certificate=ca.crt  client-certificate=cert_e
xport_rw-client.crt  client-cert-key=cert_export_rw-client.key server-address=1.1.1.1 server=ovpn-server1
```

**==> picture [13 x 13] intentionally omitted <==**

It is very important that the date on the router is within the range of the installed certificate's date of expiration. To overcome any certificate verification problems, enable NTP date synchronization on both the server and the client.
