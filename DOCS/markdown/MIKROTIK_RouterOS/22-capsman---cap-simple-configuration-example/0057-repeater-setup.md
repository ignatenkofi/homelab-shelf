## Repeater setup 

1373 

**==> picture [13 x 13] intentionally omitted <==**

Which frequency to use? 

Dual-band routers and access points, from the get-go, should have two Wi-Fi interfaces → wifi1 and wifi2, each representing a certain frequency, 5 and 2.4 GHz respectively. For repeater setup, x1 of the interfaces needs to be turned into a station interface (which will act as a client to another network), while, the other, should be set in ap mode (which will allow the device to broadcast its own network). 

If we use 2.4 GHz as a station interface, it would increase the distance at which we can install the repeater, but it would also reduce the throughput we can get from it. If we use 5 GHz as station interface, we reduce the range but increase the throughput. 

**==> picture [13 x 13] intentionally omitted <==**

Because we will be changing Wi-Fi and port-related configurations, it is advised to connect to the device's settings via Ethernet port/cable, using MAC-address. You can use Winbox "Neighbors" tab and double-click on the MAC-address of the device in the list. This way, you will not lose access later on when changing interface-related settings. 

In our example, we want to use wifi2 (2.4 GHz), as a "station" interface, while having wifi1 (5 GHz) broadcast repeater's own SSID (and also, potentially rebroadcast router's SSID over 2.4 GHz as well): 

**==> picture [505 x 244] intentionally omitted <==**
