## Sending Email 

```
/tool e-mail send
```

Send command takes the following parameters: 

**==> picture [504 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>body  (string; Default: ) The actual body of the email message<br>cc  (string; Default: ) Send a copy to listed recipients. Multiple addresses allowed, use "," to separate entries<br>file  (File[,File]; Default: ) List of the file names that will be attached to the mail separated by a comma.<br>**----- End of picture text -----**<br>

1136 

**==> picture [504 x 243] intentionally omitted <==**

**----- Start of picture text -----**<br>
from  (string; Default: ) Name or email address which will appear as the sender. If a not specified value from the server's configuration is<br>used.<br>password  (string; Default: ) Password used to authenticate to an SMTP server. If a not specified value from the server's configuration is used.<br>port  (integer[0..65535]; Default:  Port of SMTP server. If not specified, a value from the server's configuration is used.<br>)<br>server  (IP/IPv6 address;  Ip or IPv6 address of SMTP server. If not specified, a value from the server's configuration is used.<br>Default: )<br>tls  (yes|no|starttls; Default: no ) Whether to use TLS encryption:<br>yes - sends STARTTLS and drops the session if TLS is not available on the server<br>no - do not send STARTTLS<br>starttls - sends STARTTLS and continue without TLS if a server responds that TLS is not available<br>subject  (string; Default: ) The subject of the message.<br>to  (string; Default: ) Destination email address. Single address allowed.<br>user  (string; Default: ) The username used to authenticate to an SMTP server. If not specified, a value from the server's configuration is<br>used.<br>**----- End of picture text -----**<br>
