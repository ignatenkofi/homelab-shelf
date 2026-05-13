## Introduction 

MQTT and HTTP are among the most popular protocols that are used for transferring all kinds of data. Both protocols are heavily utilized in different IoT setups, and they both are supported by RouterOS. 

What kind of data, you might ask? Pretty much anything... RouterOS scripting is a very powerful tool that can help you automate your devices with the help of scheduling. 

For example, you can check your system's resource information with the help of the command `/system resource print` : 

```
/system resource print
                   uptime: 4d1h37m55s
                  version: 7.14.3 (stable)
               build-time: 2024-04-17 12:47:58
         factory-software: 6.45.9
              free-memory: 926.0MiB
             total-memory: 1024.0MiB
                      cpu: ARM
                cpu-count: 4
            cpu-frequency: 533MHz
                 cpu-load: 0%
           free-hdd-space: 88.5MiB
          total-hdd-space: 128.0MiB
  write-sect-since-reboot: 1107
         write-sect-total: 1447413
               bad-blocks: 0%
        architecture-name: arm
               board-name: RB1100AHx4
                 platform: MikroTik
```

This command shows you useful information, like CPU usage, RAM-memory usage, device's uptime and its firmware version. Another command will print out GPS coordination (if the device has a GPS chip built-in) and so on... 

What this means, essentially, is that anything that can be "printed out" into the RouterOS terminal, can be scripted to be structured into JSON format messages and send out with a configured interval. We will showcase a more detailed example later on in the guide. 

In other words, you are able to send the data from your MikroTik to any MQTT or HTTP server of your choice. Kaa IoT is one of such servers. 

Why Kaa IoT?
