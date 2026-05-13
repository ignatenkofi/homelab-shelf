## Monitor interface on the Slave AP: 

```
[admin@SlaveAP] /interface wireless> monitor wlan1
                  status: running-ap
                 channel: 5220/20/an
       wireless-protocol: nv2
             noise-floor: -110dBm
      registered-clients: 1
   authenticated-clients: 1
          nv2-sync-state: synced
         nv2-sync-master: 4C:5E:0C:57:84:38
       nv2-sync-distance: 1
    nv2-sync-period-size: 2
 nv2-sync-downlink-ratio: 50
```

Debug logs on the Master AP: 

```
09:22:08 wireless,debug wlan1: 4C:5E:0C:57:85:BE attempts to sync
```
