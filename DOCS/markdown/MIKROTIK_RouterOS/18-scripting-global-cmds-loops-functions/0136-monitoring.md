## Monitoring 

To monitor the status and performance of the PTP profile, use the following command: 

```
/system ptp monitor 0
```

The output will provide detailed information about the profile's operational status: 

1162 

```
name: ptp1
clock-id: 64:D1:54:FF:FE:EB:AD:C7
priority1: 246
priority2: 248
i-am-gm: no
gm-clock-id: 64:D1:54:FF:FE:EB:AE:C3
gm-priority1: 100
gm-priority2: 248
master-clock-id: 64:D1:54:FF:FE:EB:AE:C3
slave-port: ether1
freq-drift: 2690 ppb
offset: 3 ns
hw-offset: -889419842 ns
slave-port-delay: 306 ns
```

This information includes critical details such as the clock IDs, priority values, and timing offsets, which are essential for monitoring the accuracy and synchronization of your PTP setup.
