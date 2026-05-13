## QSFP+/QSFP28 interface supported link rates 

In RouterOS, QSFP+ and QSFP28 interfaces are designed to handle high-speed data transmission by utilizing multiple channels. Each QSFP+ or QSFP28 interface is divided into four sub-interfaces, each corresponding to a transmission channel necessary for proper operation. 

**==> picture [13 x 13] intentionally omitted <==**

The naming convention for QSFP+ and QSFP28 sub-interfaces includes two parts: 

The first digit following "qsfpplus" or "qsfp28-" represents the QSFP+ or QSFP28 physical interface. The second digit, ranging from 1 to 4, denotes each of the individual channels. 

Below are examples of how QSFP+ and QSFP28 interfaces appear in RouterOS: 

```
# QSFP+
/interface ethernet print
Flags: R - RUNNING
Columns: NAME, MTU, MAC-ADDRESS, ARP, SWITCH
 #   NAME            MTU  MAC-ADDRESS        ARP      SWITCH
 1   qsfpplus1-1    1500  48:8F:5A:B6:09:8C  enabled  switch1
 2   qsfpplus1-2    1500  48:8F:5A:B6:09:8D  enabled  switch1
 3   qsfpplus1-3    1500  48:8F:5A:B6:09:8E  enabled  switch1
 4   qsfpplus1-4    1500  48:8F:5A:B6:09:8F  enabled  switch1
# QSFP28
/interface ethernet print
Flags: R - RUNNING
Columns: NAME, MTU, MAC-ADDRESS, ARP, SWITCH
 #   NAME         MTU  MAC-ADDRESS        ARP      SWITCH
 1   qsfp28-1-1  1500  DC:2C:6E:9E:11:14  enabled  switch1
 2   qsfp28-1-2  1500  DC:2C:6E:9E:11:15  enabled  switch1
 3   qsfp28-1-3  1500  DC:2C:6E:9E:11:16  enabled  switch1
 4   qsfp28-1-4  1500  DC:2C:6E:9E:11:17  enabled  switch1
```

Configuration and monitoring for these sub-interfaces may vary based on factors such as auto-negotiation, advertised speeds, and the type of transceiver (e.g., break-out cable or single fiber). The following sections will provide guidance on the configuration necessary for each use case. 

1319 

**==> picture [13 x 13] intentionally omitted <==**

Disabling or enabling any of the four sub-interfaces will trigger a reconfiguration of the entire port group, restarting all four channels.
