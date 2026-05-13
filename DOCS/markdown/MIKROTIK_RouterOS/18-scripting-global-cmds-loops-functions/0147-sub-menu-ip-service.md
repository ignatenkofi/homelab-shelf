## Sub-menu: `/ip service` 

**==> picture [509 x 219] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP address List of IP/IPv6 prefixes from which the service is accessible. When this parameter is set, packets are not dropped at the<br>/netmask | IPv6/0..128;  network level, but access to the service is denied for sources not matching the specified addresses.<br>Default: ) This option is best suited for restricting access within trusted networks.<br>To block access from external or untrusted networks, we recommend using a Firewall instead.<br>certificate  (name; Default: n The name of the certificate used by a particular service. Applicable only for services that depend on certificates (www-<br>one ) ssl, api-ssl)<br>name  (name; Default: none ) Service name<br>max-sessions   (integer: 1.. Max simultaneous session count for service<br>1000; Default: 20)<br>port  (integer: 1..65535;  The port particular service listens on<br>Default: )<br>tls-version  (any | only-1.2;  Specifies which TLS versions to allow by a particular service<br>Default: any )<br>**----- End of picture text -----**<br>


1168 

vrf (name; Default: main ) Specify which VRF instance to use by a particular service
