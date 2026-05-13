## GUI setup 

Connect to your router via Winbox or WebFig. 

Winbox can be downloaded in the link given below: 

https://mikrotik.com/download 

**==> picture [505 x 227] intentionally omitted <==**

It is Highly recommended to upgrade your RouterOS version to the latest available. Installing the version will perform a reboot: 

1617 

**==> picture [505 x 361] intentionally omitted <==**

If your device does not have IoT>LoRa menu, download " Extra packages " specifically for your routers architecture and rOS version. You can see the type of your routers architecture at the top of Winbox window or in System →  Resources → Architecture Name. 

https://mikrotik.com/download 

1618 

**==> picture [505 x 302] intentionally omitted <==**

Once the package is downloaded and extracted, upload the IoT package to your router. It can be done via drag & drop as well. It should appear in the files folder after the upload is complete, reboot your router (System → Reboot) to install the package: 

1619 

**==> picture [505 x 377] intentionally omitted <==**

After the reboot, the package should be visible in the Package list: 

1620 

**==> picture [505 x 364] intentionally omitted <==**

Check if the LoRa gateway has initialized under IoT>LoRa>Devices . If it is LtAP model, make sure to set USB Type to Mini-PCIe: 

1621 

**==> picture [505 x 339] intentionally omitted <==**

Once the gateway has shown up (under IoT>LoRa>Devices ) select it, choose Network Servers from the default ones or add your own (under IoT>LoRa>Se rvers ) and enable it: 

**==> picture [505 x 281] intentionally omitted <==**

Navigate to Traffic tab to monitor the surrounding nodes sending requests: 

1622 

**==> picture [505 x 177] intentionally omitted <==**

This concludes basic installation and configuration of LoRa mini-PCIe cards. For additional settings check: General Properties 

1623
