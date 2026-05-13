## Log messages 

SNTP client can produce the following log messages. See the article "log" on how to set up logging and how to inspect logs. 

- ntp , debug gradually adjust by OFFS ntp , debug instantly adjust by OFFS ntp , debug Wait for N seconds before sending the next message ntp , debug Wait for N seconds before restarting ntp , debug , packet packet receive an error, restarting ntp , debug , packet received PKT ntp , debug , packet ignoring received PKT ntp , debug , packet error sending to IP, restarting ntp , debug , packet sending to IP PKT 

Explanation of log message fields 

OFFS - difference of two NTP timestamp values, in hexadecimal. 

1156 

PKT - dump of NTP packet. If the packet is shorter than the minimum 48 bytes, it is dumped as a hexadecimal string. Otherwise, the packet is dumped as a list of field names and values, one per log line. Names of fields follow RFC4330. IP - remote IP address. 

NOTE : the above logging rules work only with the built-in SNTP client, the separate NTP package doesn't have any logging facilities. 

1157
