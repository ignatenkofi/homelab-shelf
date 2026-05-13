## Restrict station connections only to specific access points 

Set value of default-authentication interface property to no. 

/interface wireless set station-wlan default-authentication=no 

Create rules that matches allowed access points. These rules must have connect =yes and interface equal to the name of station wireless interface. 

/interface wireless connect-list add interface=station-wlan connect=yes mac-address=00:11:22:33:00:01/interface wireless connectlist add interface=station-wlan connect=yes mac-address=00:11:22:33:00:02
