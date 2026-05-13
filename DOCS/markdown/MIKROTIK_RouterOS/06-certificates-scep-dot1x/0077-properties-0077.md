## Properties 

**==> picture [516 x 181] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>caller-id  (string; Default: ) For PPTP and L2TP it is the IP address a client must connect from. For PPPoE it is the MAC address (written in CAPITAL<br>letters) a client must connect from. For ISDN it is the caller's number (that may or may not be provided by the operator) the<br>client may dial-in from<br>comment  (string; Default:  Short description of the user.<br>)<br>disabled  (yes | no;  Whether secret will be used.<br>Default:  no )<br>limit-bytes-in  (integer;  The maximum amount of bytes for a session that the client can upload.<br>Default: ) 0<br>limit-bytes-out  (integer;  The maximum amount of bytes for a session that the client can download.<br>Default: ) 0<br>**----- End of picture text -----**<br>


310 

**==> picture [516 x 247] intentionally omitted <==**

**----- Start of picture text -----**<br>
local-address  (IP address; IP address that will be set locally on ppp interface.<br>Default: )<br>name  (string; Default: ) Name used for authentication<br>password  (string; Default:  Password used for authentication<br>)<br>profile  (string; Default:  def Which user profile to use<br>ault )<br>remote-address  (IP;  IP address that will be assigned to the remote ppp interface.<br>Default: )<br>remote-ipv6-prefix  (IPv6  IPv6 prefix assigned to ppp client. Prefix is added to ND prefix list enabling stateless address auto-configuration on ppp<br>prefix; Default: ) interface.<br>routes  (string; Default: ) Routes that appear on the server when the client is connected. The route format is: dst-address gateway metric (for<br>example, 10.1.0.0/ 24 10.0.0.1 1). Other syntax is not acceptable since it can be represented incorrectly. Several routes<br>may be specified and separated with commas. This parameter will be ignored for OpenVPN.<br>service  (any | async |  Specifies the services that a particular user will be able to use.<br>isdn | l2tp | pppoe | pptp |<br>ovpn | sstp; Default:  any )<br>**----- End of picture text -----**<br>
