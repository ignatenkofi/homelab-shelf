## PPPoE Connection 

PPPoE connection also gives you a dynamic IP address and can configure dynamically DNS and default gateway. Typically service provider (ISP) gives you a username and password for the connection 

```
/interface pppoe-client
```

```
  add disabled=no interface=ether1 user=me password=123 \
    add-default-route=yes use-peer-dns=yes
```

Winbox/WebFig actions: 

In the PPP window, select the Interfaces tab and click the "+" button; Choose PPPoE Client from the dropdown list; Set the name and select ether1 as the interface; Go to the Dial Out tab, configure the username, password, and other parameters; Click OK to save the settings. 

**==> picture [505 x 160] intentionally omitted <==**

22 

**==> picture [218 x 215] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

Further in configuration, the WAN interface is now the pppoe-out1 interface, not ether1 .
