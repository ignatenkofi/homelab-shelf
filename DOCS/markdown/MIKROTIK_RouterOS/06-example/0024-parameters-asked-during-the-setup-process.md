## Parameters asked during the setup process 

**==> picture [500 x 82] intentionally omitted <==**

**----- Start of picture text -----**<br>
Parameter Description<br>hotspot interface  (string;  Interface name on which to run HotSpot. To run HotSpot on a bridge interface, make sure public interfaces are<br>Default: allow ) not included in the bridge ports.<br>local address of network  (IP;  HotSpot gateway address<br>Default: 10.5.50.1/24 )<br>**----- End of picture text -----**<br>


292 

**==> picture [500 x 226] intentionally omitted <==**

**----- Start of picture text -----**<br>
masquerade network  (yes | no;  Whether to masquerade HotSpot network, when yes rule is added to /ip firewall nat with action=masquerade<br>Default: yes )<br>address pool of network  (string; Address pool for HotSpot network, which is used to change user IP address to a valid address. Useful if<br>Default: yes ) providing network access to mobile clients that are not willing to change their networking settings.<br>select certificate  (none | import- Choose SSL certificate, when HTTPS authorization method is required.<br>other-certificate; Default: )<br>ip address of smtp server  (IP;  The IP address of the SMTP server, where to redirect HotSpot's network SMTP requests (25 TCP port)<br>Default: 0.0.0.0 )<br>dns servers  (IP; Default: 0.0.0.0 DNS server addresses used for HotSpot clients, configuration taken from /ip dns menu of the HotSpot gateway<br>)<br>dns name  (string; Default: "" ) the domain name of the HotSpot server, a full qualified domain name is required, for example, www.example.com<br>name of local hotspot user  (stri username of one automatically created HotSpot user, added to /ip hotspot user<br>ng; Default: "admin" )<br>password for the user'  (string;  Password for automatically created HotSpot user<br>Default: )<br>**----- End of picture text -----**<br>
