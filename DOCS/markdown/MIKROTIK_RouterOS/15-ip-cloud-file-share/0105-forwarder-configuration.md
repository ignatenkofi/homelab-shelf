## Forwarder configuration 

In /ip/dns/forwaders section, forwarders can added, modified or removed. 

**==> picture [516 x 120] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string; Default: ) Forwarder name.<br>dns-servers  (string; Default: ) An IP address or DNS name of a domain name server. Can contain multiple records, for example, dns-servers=1.<br>1.1.1,8.8.8.8,local.dns<br>doh-servers  (string; Default: ) A URL of DoH server. Can contain multiple records.<br>verify-doh-cert  (yes | no;  Specifies whether to validate the DoH server, when one is being used. Will use the "/certificate" list in order to verify<br>Default: yes) server validity.<br>**----- End of picture text -----**<br>
