## Enable QoS hardware offloading for the above settings to start working. 

```
/interface ethernet switch
set switch1 qos-hw-offloading=yes
```

Enable the LLDP Data Center Bridging Capability Exchange Protocol (DCBX) to share QoS settings and capabilities with other neighboring devices. 

```
/ip neighbor discovery-settings
set lldp-dcbx=yes
```

As an optional step, increase the L2MTU to accommodate larger data packets. 

```
/interface ethernet
set [find switch=switch1] l2mtu=9500
```

463
