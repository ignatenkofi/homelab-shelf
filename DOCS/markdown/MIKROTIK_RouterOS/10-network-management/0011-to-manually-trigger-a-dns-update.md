## To manually trigger a DNS update: 

```
[admin@MikroTik] > /ip cloud force-update
```

**==> picture [13 x 13] intentionally omitted <==**

To actually connect to the device using the DNS name provided by the cloud server, a user must configure the router's firewall to permit such access from the WAN port. (Default MikroTik configuration does not permit access to services such as WebFig, WinBox, etc. from the WAN port).
