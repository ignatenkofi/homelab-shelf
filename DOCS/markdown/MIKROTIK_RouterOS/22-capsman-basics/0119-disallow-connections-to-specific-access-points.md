## Disallow connections to specific access points 

Set value of default-authentication interface property to yes. 

/interface wireless set station-wlan default-authentication=yes 

Create connect =no rules that match those access points that station should not connect to. These rules must have connect =no and interface equa l to the name of station wireless interface. 

/interface wireless connect-list add interface=station-wlan connect=no mac-address=00:11:22:33:44:55
