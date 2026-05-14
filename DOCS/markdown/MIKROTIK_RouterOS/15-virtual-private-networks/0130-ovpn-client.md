## OVPN Client 

**==> picture [516 x 147] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>add-default-route  (yes  no| ; Default:  no ) Whether to add OVPN remote address as a default route.<br>auth  (md5  sha1  null  sha256  sha512| | | | ; Default:  sha1 ) Allowed authentication methods.<br>certificate  (string  none| ; Default:  none ) Name of the client certificate<br>cipher  (null | aes128-cbc | aes128-gcm | aes192-cbc | aes192-gcm |  Allowed ciphers. In order to use GCM type ciphers, the "auth" parameter must<br>aes256-cbc | aes256-gcm | blowfish128; Default:  blowfish128 ) be set to "null", because GCM cipher is also responsible for "auth", if used.<br>comment  (string; Default: ) Descriptive name of an item<br>connect-to  (IP|IPv6; Default: ) Remote address of the OVPN server.<br>**----- End of picture text -----**<br>

1244 

**==> picture [516 x 328] intentionally omitted <==**

**----- Start of picture text -----**<br>
disabled  (yes  no| ; Default:  yes ) Whether the interface is disabled or not. By default it is disabled.<br>mac-address  (MAC; Default: ) Mac address of OVPN interface. Will be automatically generated if not specified.<br>max-mtu  (integer; Default:  1500 ) Maximum Transmission Unit. Max packet size that the OVPN interface will be<br>able to send without packet fragmentation.<br>mode  (ip  ethernet| ; Default: ) ip Layer3 or layer2 tunnel mode (alternatively tun, tap)<br>name  (string; Default: ) Descriptive name of the interface.<br>password  (string; Default: ) "" Password used for authentication. Value of password should not be longer than<br>1000 chars.<br>port  (integer; Default:  1194 ) Port to connect to.<br>profile  (name; Default:  default ) Specifies which PPP profile configuration will be used when establishing the<br>tunnel.<br>protocol  (tcp  udp| ; Default:  tcp ) indicates the protocol to use when connecting with the remote endpoint.<br>verify-server-certificate  (yes  no| ; Default:  no ) Checks the certificates CN or SAN against the "connect-to" parameter. The IP or<br>hostname must be present in the server's certificate.<br>tls-version  (any  only-1.2| ; Default:  any ) Specifies which TLS versions to allow<br>use-peer-dns  (yes  no| ; Default:  no ) Whether to add DNS servers provided by the OVPN server to IP/DNS<br>configuration.<br>route-nopull  (yes  no| ; Default:  no ) Specifies whether to allow the OVPN server to add routes to the OVPN client<br>instance routing table.<br>user  (string; Default: ) User name used for authentication.<br>**----- End of picture text -----**<br>

Also, it is possible to import the OVPN client configuration from a .ovpn configuration file. Such a file usually is provided from the OVPN server side and already includes configuration so you need to worry only about a few parameters. 

```
/interface/ovpn-client/import-ovpn-configuration ovpn-password=securepassword \
key-passphrase=certificatekeypassphrase ovpn-user=myuserid skip-cert-import=no
```

OVPN client supports tls authentication. The configuration of tls-auth can be added only by importing .ovpn configuration file. Using tls-auth requires that you generate a shared-secret key, this key should be added to the client configuration file .ovpn. 

Note* ROS client requires user name and password. Authentication is managed by server side, if its supports tls, then user name will be ignored. 

```
key-direction 1
<tls-auth>
#
# 2048 bit OpenVPN static key
#
-----BEGIN OpenVPN Static key V1-----
-----END OpenVPN Static key V1-----
</tls-auth>
```

```
7.17beta5 added support to allow non-null auth in gcm mode.
```
