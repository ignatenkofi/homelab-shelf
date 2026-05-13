## Wireless Debug Logs 

Debugging wireless problems using Logs. 

By default RouterOS wireless log shows that client connects and disconnects as simple entries: 

```
22:32:18 wireless,info 00:80:48:41:AF:2A@wlan1: connected
```

It is enough for regular users to know that the wireless client with MAC address "00:80:48:41:AF:2A" is connected to wireless interface "wlan1". But actually there are more log entries available than are shown in standard logging. They are called 'debug' logs which give more detailed information. In the following Debug Log example you will see the same client connecting to the AP in more detail than found in typical logging: 

```
22:33:20 wireless,debug wlan1: 00:80:48:41:AF:2A attempts to connect
22:33:20 wireless,debug wlan1: 00:80:48:41:AF:2A not in local ACL, by default accept
22:33:20 wireless,info 00:80:48:41:AF:2A@wlan1: connected
```

Debug Logs will give you more specific information on each step of the Client wireless connection and disconnection. The first line shows that the wireless client tried to connect to the AP. On the second line the AP checked to see if that client is allowed to connect to the AP and the resulting action. And only on the third line do you see that the client is connected. This is merely one example of the debug log messages. The description of all debug entries is written below. 

To enable the wireless debug logs you should execute such commands: 

```
[admin@MikroTik] > /system logging
```

```
[admin@MikroTik] system logging> add topics=wireless,debug action=memory
```

This will help you understand and fix wireless problems with ease and with less interaction with the support team.
