## VirtualAP 

It is possible to create virtual access points using the add command in the wireless menu. You must specify the master-interface which the virtual interface will belong to. If "master-interface" mode is "station", Virtual AP will work only when "master-interface" will be active. The Virtual AP can have it's own SSID and Security Profile. 

Virtual AP interface will only work if master interface is in ap-bridge  bridge  station , , or wds-slave mode. It works only with 802.11 protocol, Nv2 is not supported. 

This feature is useful for separating access for different types of users. You can assign different bandwidth levels and passwords and instruct users to connect to the specific virtual network, it will appear to wireless clients as a different SSID or a different device. For example, when using QuickSet to configure a guest network, the VirtualAP feature is used in the background. 

To create a new virtual-ap: `/interface> wireless add mode=ap-bridge master-interface=wlan1 ssid=guests securityprofile=guests` (such security profile first needs to be created) 

Note: you can create up to 127 virtual interfaces per physical interface. It is not recommended to create more 30, since the performance will start to degrade.
