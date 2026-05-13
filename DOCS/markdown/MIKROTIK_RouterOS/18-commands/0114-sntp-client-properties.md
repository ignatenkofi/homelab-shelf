## SNTP Client properties: 

**==> picture [516 x 272] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (yes, no  Enable SNTP client for time synchronization<br>default: no)<br>mode  (broadcast,  Mode that the SNTP client will operate in. If no NTP servers are configured broadcast mode will be used. If there is a dynamic<br>unicast, filed is read- or static NTP server IP address or FQDN used it will automatically switch to unicast mode.<br>only)<br>primary-ntp  (IP  IP address of the NTP server that has to be used for time synchronization. If both values are non-zero, then the SNTP client will<br>address default: 0.0.0 alternate between the two server addresses, switching to the other when the request to the current server times out or when the<br>.0) "KoD" packet is received, indicating that the server is not willing to respond to requests from this client.<br>The following formats are accepted:<br>- ipv4<br>- ipv6<br>secondary-ntp  (IP  see  primary-ntp<br>address default: 0.0.0<br>.0)<br>server-dns-names  (C To set the NTP server using its domain name. The domain name will be resolved each time an NTP request is sent. Router has<br>omma separated  to have /ip dns configured.<br>domain name list<br>default: )<br>**----- End of picture text -----**<br>


Status 

active-server (IP address; read-only property) : Currently selected NTP server address. This value is equal to primary-ntp or secondary-ntp . poll-interval (Time interval; read-only property) : Current interval between requests sent to the active server. The initial value is 16 seconds, and it is increased by doubling to 15 minutes. 

Last received packet information 

Values of the following properties are reset when the SNTP client is stopped or restarted, either because of a configuration change, or because of a network error. 

last-update-from (IP address; read-only property) : Source IP address of the last received NTP server packed that was successfully processed. 

1153 

last-update-before (Time interval; read-only property) : Time since the last successfully received server message. 

- last-adjustment (Time interval; read-only property) : Amount of clock adjustment that was calculated from the last successfully received NTP server message. 

last-bad-packet-from (IP address; read-only property) : Source IP address of last received SNTP packed that was not successfully processed. Reason of the failure and time since this packet was received is available in the next two properties. 

last-bad-packet-before (Time interval; read-only property) : Time since the last receive failure. 

last-bad-packet-reason (Text; read-only property) : Text that describes the reason of the last receive failure. Possible values are: 

- bad-packet-length - Packet length is not in the acceptable range. 

- server-not-synchronized - Leap Indicator field is set to "alarm condition" value, which means that clock on the server has not been synchronized yet. 

zero-transmit-timestamp - Transmit Timestamp field value is 0. 

bad-mode - Value of the Mode field is neither 'server' nor 'broadcast'. 

- kod-ABCD - Received "KoD" (Kiss-o'-Death) response. ABCD is the short "kiss code" text from the Reference Identifier field. 

- broadcast - Received broadcast message, but mode =unicast. 

- non-broadcast - Received packed was server reply, but mode =broadcast. 

- server-ip-mismatch - Received response from address that is not active-server . 

originate-timestamp-mismatch - Originate Timestamp field in the server response message is not the same as the one included in the last request. 

roundtrip-too-long - request/response roundtrip exceeded 1 second.
