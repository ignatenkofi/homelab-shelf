## Monitoring 

857 

Command `/interface vpls monitor [id]` will display the current VPLS interface status 

For example: `[admin@10.0.11.23] /interface vpls> monitor vpls2 remote-label: 800000 local-label: 43 remote-status: transport: 10.255.11.201/32 transport-nexthop: 10.0.11.201 imposed-labels: 800000` 

Available read-only properties: 

**==> picture [411 x 155] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>imposed-label  (integer) VPLS imposed label<br>local-label  (integer) Local VPLS label<br>remote-group  ()<br>remote-label  (integer) Remote VPLS label<br>remote-status  (integer)<br>transport-nexthop  (IP prefix) Shows used transport address (typically Loopback address).<br>transport  (string) Name of the transport interface. Set if VPLS is running over the Traffic Engineering tunnel.<br>**----- End of picture text -----**<br>


858
