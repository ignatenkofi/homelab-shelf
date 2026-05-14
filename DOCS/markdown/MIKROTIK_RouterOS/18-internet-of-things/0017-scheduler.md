## Scheduler 

Apply a scheduler to the script, so that RouterOS periodically initiates the script by itself: 

```
/system/scheduler/add name=bluetoothscheduler interval=30s on-event="/system/script/run tracking"
```

You can set up shorter and longer intervals. If you want to send data more often, so that the data is "fresher" →  set up shorter time intervals (10-15 seconds). If you want to send fewer messages, less often → you can set up longer time intervals (30min+). 

The JSON message structured using the script has a " `ts` " value (timestamp) assigned for each payload received. Meaning that when the script is run , for example, every minute , 1 tag is used and the tag broadcasts 1 payload every 10 seconds (that is 6 payloads per minute ) → ThingsBoard data (GUI) will be updated every minute, and every minute, 6 new entries will appear (each entry will indicate that it was received 10 seconds after the previous one). And if you send the message every 15 minutes when using 1 tag that is broadcasting a payload every 10 seconds (that is 6*15=90 payloads per 15 minutes) → ThingsBoard data (GUI) will be updated every 15 minutes but 90 entries will appear.
