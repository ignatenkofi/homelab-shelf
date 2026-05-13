## Actions 

Sub-menu level: **`/system logging action`** 

**==> picture [516 x 91] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>cef-event-delimiter  (string; Default:  \r\n ) option helps remote syslog to distinguish between individual events within sent<br>batch<br>disk-file-count  (integer [1..65535]; Default: ) 2 specifies number of files used to store log messages, applicable only if action=disk<br>disk-file-name  (string; Default:  log ) name of the file used to store log messages, applicable only if action=disk<br>**----- End of picture text -----**<br>


1772 

**==> picture [516 x 647] intentionally omitted <==**

**----- Start of picture text -----**<br>
disk-lines-per-file  (integer [1..65535]; Default:  100 ) specifies maximum size of file in lines, applicable only if action=disk<br>disk-stop-on-full  (yes|no; Default:  no ) whether to stop to save log messages to disk after the specified disk-lines-per-file<br>and disk-file-count number is reached, applicable only if action=disk<br>email-start-tls  (yes | no; Default:  no ) Whether to use tls when sending email, applicable only if action=email<br>email-to  (string; Default: ) email address where logs are sent, applicable only if action=email<br>memory-lines  (integer [1..65535]; Default:  1000 ) number of records in local memory buffer, applicable only if action=memory<br>memory-stop-on-full  (yes|no; Default:  no ) whether to stop to save log messages in local buffer after the specified memory-<br>lines number is reached<br>name  (string; Default: ) name of an action. When target=memory, this name also serves as the identifier<br>for a specific memory buffer. Multiple actions with target=memory can be created,<br>each storing logs in its own separate buffer.<br>remember  (yes|no; Default: ) whether to keep log messages, which have not yet been displayed in console,<br>applicable if action=echo<br>remote-log-format  (cef, default, syslog; Default:  default ) Format for logs to be sent to remote instance:<br>cef - logs are sent in CEF format;<br>default - logs are sent as it is;<br>syslog - logs are sent in BSD-syslog format<br>remote-port  (IP/IPv6 Address[:Port]; Default:  0.0.0.0:514 ) remote logging server's IP/IPv6 address and UDP port, applicable if action=remote<br>remote-protocol  (tcp / udp; Default:  udp )  protocol for remote logging messages, tcp only works with CEF remote-log-<br>format, for syslog it will always use UDP, even if TCP is set<br>src-address  (IP address; Default:  0.0.0.0 ) source address used when sending packets to remote server<br>syslog-facility  (auth, authpriv, cron, daemon, ftp, kern, local0,<br>local1, local2, local3, local4, local5, local6, local7, lpr, mail, news,<br>ntp, syslog, user, uucp; Default:  daemon )<br>syslog-severity  (alert, auto, critical, debug, emergency, error, info,  Severity level indicator defined in RFC 3164:<br>notice, warning; Default:  auto )<br>Emergency: system is unusable<br>Alert: action must be taken immediately<br>Critical: critical conditions<br>Error: error conditions<br>Warning: warning conditions<br>Notice: normal but significant condition<br>Informational: informational messages<br>Debug: debug-level messages<br>syslog-time-format  (bsd-syslog, iso8601; Default:  bsd-syslog ) Timelog format for messages<br>target  (disk, echo, email, memory, remote; Default:  memory ) storage facility or target of log messages<br>disk - logs are saved to the hard drive<br>echo - logs are displayed on the console screen<br>email - logs are sent by email<br>memory - logs are stored in local memory buffer or multiple seperate buffers<br>(RAM files).<br>remote - logs are sent to remote host<br>vrf  (name; Default: main ) Set VRF on which the remote logging is making outgoing connections, applicable<br>only if target=remote. The setting is available since RouterOS version 7.19.<br>**----- End of picture text -----**<br>


Create seperate memory logging buffers 

1773 

Just like having different text files for different notes, these separate memory buffers allow you to direct specific types of log messages (based on topics) into distinct storage areas in memory. 

Isolation: Logs sent to `buffer_A` are completely separate from logs sent to `buffer_B` . Independent Viewing: You can view the contents of just one buffer at a time using `/log print where buffer=buffer_name` . Targeted Clearing: You can clear the contents of one specific buffer using `/system logging action clear action=buffer_name` without affecting the logs stored in any other memory buffer. 

This provides much better organization and control over logs stored in memory, especially for debugging or monitoring, without mixing them all into the single default memory log. 

Sub-menu level: **`/system logging action clear`** 

Starting from 7.20_ab244, memory logs (target=memory) can be cleared with command: /system logging action clear action=< **`logging`** action name>
