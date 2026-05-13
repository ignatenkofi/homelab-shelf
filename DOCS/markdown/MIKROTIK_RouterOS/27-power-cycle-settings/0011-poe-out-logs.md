## PoE-Out Logs 

By default PoE-Out, event logging is enabled and uses "warning" and "info" topics to notify the user about PoE-Out state changes. Log entries will be added to each PoE-Out state change. Important logs will be added with a "warning" topic, informative logs will be added with the "info" topic.  When PoE LLDP is enabled, LLDP status updates are available in the device logs, for example: 

**==> picture [13 x 13] intentionally omitted <==**

```
06:56:50 poe-out,debug ether4 LLDP TLV 25.0W request denied : hw-limit
```

Possible denial reasons: 

**==> picture [13 x 13] intentionally omitted <==**

- budget requested power exceeds the total PSE budget. 

hw-limit - requested power is more than hardware supports (PSU affects this). low-voltage - LLDP request made to low-voltage port. 

off - port is shut down. class-limit - LLDP requires more than the class can provide. cmd-failed - RouterOS could not make a request to the controller. 

To avoid unnecessary logging in cases when PD is not powered because of current-too-low, RouterOS will filter such events, and add one log per every 512 current-too-low events. 

Logs can be disabled if necessary: 

**==> picture [13 x 13] intentionally omitted <==**

/system logging set [find topics~"info"] topics=info,!poe-out /system logging set [find topics~"warning"] topics=warning,!poe-out
