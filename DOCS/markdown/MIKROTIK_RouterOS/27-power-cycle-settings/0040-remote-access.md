## Remote Access 

Sub-menu: `/port remote-access` 

If you want to access serial device that can only talk to COM ports and is located somewhere else behind router, then you can use remote-access. As defined in RFC 2217 RouterOS can transfer data from/to a serial device over TCP connection. 

Enabling remote access on RouterOS is very easy: 

```
/port remote-access add port=serial0 protocol=rfc2217 tcp-port=9999
```

**==> picture [13 x 13] intentionally omitted <==**

By default serial0 is used by serial-terminal. Without releasing the port, it cannot be used by remote-access or other services
