## To make Nv2 synced setup: 

- For Nv2 Synchronization a Master Nv2 AP should be chosen and "nv2-mode=sync-master" should be specified together with "nv2-sync-secret". For Nv2 Slave APs the same wireless frequency as Master AP should be used and "nv2-mode=sync-slave" should be specified with the same "nv2-sync-secret" as the in Master AP configuration. 

- When Master AP is enabled Slave APs will try start searching for Master AP by matching it against specified "nv2-sync-secret". After Master AP is found the Slave AP will calculate the distance to the Master AP as it is possible that Master AP is located not on the same location. 

- Then Slave AP starts operating as AP and it adapts the period size and downlink ratio from the synced Master AP. In addition after the Slave AP is operational other Slave APs can use this Slave AP to sync with. 

- Slave AP periodically listens for the Master AP and checks if the "nv2-sync-secret" still matches and adapts the parameters again. If Master AP interface is disabled/enabled all the Slaves will be also disabled and will start the synchronization process from the beginning. If Master AP stops working Slave APs also will stop working as they do not have sync information.
