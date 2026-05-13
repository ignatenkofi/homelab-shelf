## Properties 

```
/tool e-mail
```

This submenu allows setting SMTP server that will be used. 

**==> picture [502 x 204] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP/IPv6 address; Default: 0.0.0.0 ) SMTP server's IP address.<br>from  (string; Default: <> ) Name or email address that will be shown as a receiver.<br>password  (string; Default: "" ) Password used for authenticating to an SMTP server.<br>port  (integer[0..65535]; Default: 25 ) SMTP server's port.<br>tls  (no|yes|starttls; Default: no ) Whether to use TLS encryption:<br>yes - sends STARTTLS and drops the session if TLS is not available on the server<br>no - do not send STARTTLS<br>starttls - sends STARTTLS and continue without TLS if a server responds that TLS is not available<br>user  (string; Default: "" ) The username used for authenticating to an SMTP server.<br>vrf  (VRF name; default value: main ) Set VRF on which service is creating outgoing connections.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

Note: All server's configurations (if specified) can be overridden by send command.
