## Connect List 

Sub-menu: `/interface wireless connect-list` 

connect-list is used to assign priority and security settings to connections with remote access points, and to restrict allowed connections. connect-list is an ordered list of rules. Each rule in connect-list is attached to specific wireless interface, specified in the `interface` property of that rule (this is unlike access -list, where rules can apply to all interfaces). Rule can match MAC address of remote access point, it's signal strength and many other parameters. 

Operation: 

- connect-list rules are always checked sequentially, starting from the first. disabled rules are always ignored. 

- Only the first matching rule is applied. 

- If SSID or exact wireless protocol is provided in the wireless interface configuration Connect List SSIDs or wireless protocols not covered by wireless interface configuration are ignored. 

- If connect-list does not have any rule that matches remote access point, then the default values from the wireless interface configuration are used. If access point is matched by rule that has connect =no value, connection with this access point will not be attempted. If access point is matched by rule that has connect =yes value, connection with this access point will be attempted. In station mode, if several remote access points are matched by connect list rules with connect =yes value, connection will be attempted with access point that is matched by rule higher in the connect-list. If no remote access points are matched by connect-list rules with connect =yes value, then value of default-authentication interface property determines whether station will attempt to connect to any access point. If default-authentication =yes, station will choose access point with best signal and compatible security. 

In access point mode, connect-list is checked before establishing WDS link with remote device. If access point is not matched by any rule in the connect list, then the value of default-authentication determines whether WDS link will be established.
