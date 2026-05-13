## mPCIe modems with RB9xx series devices 

In case your modem is not being recognized after a soft reboot, then you might need to add a delay before the USB port is initialized. This can be done using the following command: 

```
/system routerboard settings set init-delay=5s
```
