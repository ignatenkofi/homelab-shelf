## PPP Client example 

This is an example of how to add a client using an exposed serial port from an LTE modem. 

```
/interface ppp-client add apn=yourapn dial-on-demand=no disabled=no port=usb2
```

The dial-on-demand should to be set to 'no' for a continuous connection.
