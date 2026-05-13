## Parameters 

**==> picture [500 x 192] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>arp  (disabled |  ARP resolution protocol mode.<br>enabled | proxy-<br>arp | reply-only;<br>Default: enabled )<br>arp-timeout  (integ<br>er; Default: auto)<br>authentication  (ah Authentication method to use for VRRP advertisement packets.<br>| none | simple;<br>Default: none ) none  - should be used only in low-security networks (e.g., two VRRP nodes on LAN).<br>ah  - IP Authentication Header. This algorithm provides strong protection against configuration errors, replay attacks, and<br>packet corruption/modification. Recommended when there is limited control over the administration of nodes on a LAN.<br>HMAC-MD5 is used.<br>simple  - uses a clear-text password. Protects against accidental misconfiguration of routers on a local network.<br>**----- End of picture text -----**<br>


788 

connectionSpecifies the mode for connection tracking synchronization. This setting is only relevant when `sync-connection-` tracking-mode (ac `tracking=yes` is enabled. tive-active | passive-active; `passive-active` - this mode is designed for traditional VRRP setups, where one master and one or more backup Default: passiverouters are used. In this mode, only the master device performs connection tracking synchronization by sending updates active ) to the backup devices. Backup devices do not send any connection tracking data. `active-active` - This mode is intended for setups using multiple VRRP groups to achieve load balancing. Each VRRP group has its own master, and these masters may reside on different physical devices. With `active-active` mode, all active masters can synchronize connection tracking data with each other. Each VRRP group in active-active mode must use a unique `connection-tracking-port` value. Reusing the same port across multiple groups can cause nonsynchronized connection tracking table. Using multiple VRRP groups with `passive-active` mode may lead to unsynchronized connection tracking tables, since only one master handles synchronization, and the others do not exchange tracking data.
