## Mode station-bridge 

This mode works only with RouterOS APs and provides support for transparent protocol-independent L2 bridging on the station device. RouterOS AP accepts clients in station-bridge mode when enabled using bridge-mode parameter. In this mode, the AP maintains a forwarding table with information on which MAC addresses are reachable over which station device. 

This mode is MikroTik proprietary and cannot be used to connect to other brands of devices. 

This mode is safe to use for L2 bridging and is the preferred mode unless there are specific reasons to use station-wds mode. With station-bridge mode, it is not possible to connect to CAPsMAN controlled CAP. 

1537
