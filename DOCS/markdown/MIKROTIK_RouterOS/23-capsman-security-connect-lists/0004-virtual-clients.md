## Virtual Clients 

Note: Starting from 6.35 only in wireless-rep or wireless-cm2 package 

It is also possible to create virtual clients and have both an AP and a Client on the same physical interface. This allows to make a repeater setup with only using one hardware card. The process of configuration is exacly the same as above, but use mode station : 

To create a new virtual-client: `/interface> wireless add mode=station master-interface=wlan1 ssid=where-to-connect securityprofile=your-profile` (such security profile first needs to be created) 

Note: Virtual interfaces will always use the Master interface wireless frequency. If the Master interface has 'auto' frequency enabled it will use the wireless frequency that the Master interface selected. 

1420
