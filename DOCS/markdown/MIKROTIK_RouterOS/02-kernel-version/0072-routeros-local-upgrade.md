## RouterOS local upgrade 

Sub-menu: `system/package/local-update/` 

45 

You can upgrade one or multiple MikroTik routers within your local network by using one device which have all needed packages. Feature is available from 7.17beta3 version in (system > packages local update) and will replace (system > auto update) feature. Here is a simple example with 3 routers (the same method works on networks with infinite numbers of routers): 

Place needed packages under Files menu, on your main router: 

**==> picture [301 x 189] intentionally omitted <==**

Optional , you can set mirror device between main one, if not needed, skip this step: 

Choose Local Package Sources and enable Mirror device. Set Primary Server where the packages are located, 10.155.136.50. Check Interval min imum setting can be set to 00:07:12, at which device will connect using Winbox to a main device and check for packages. If new packages are available, it will begin to download, please note download process is slow and may require some time when large amount of files are used. In case some failures, download will resume on next Check. 

**==> picture [301 x 188] intentionally omitted <==**

New "packs" folder is created, where mirror device will store packages: 

46 

**==> picture [301 x 188] intentionally omitted <==**

Add new package source on device which will be updated, in this example we use mirror device 10.155.136.71: 

**==> picture [301 x 188] intentionally omitted <==**

Once you click Refresh in Local Update packages tab,  device using Winbox will try to connect to source and check if there are new packages. 

**==> picture [301 x 188] intentionally omitted <==**

Choose packages and click download, after download completes device will be needed to reboot for update. 

47 

**==> picture [301 x 188] intentionally omitted <==**

Use system/package/local-update/refresh to automate this in your scripts and tools fetch url= can be used to download packages from our web page, for example: tool/fetch url=https://download.mikrotik.com/routeros/7.16.1/routeros-7.16.1-arm.npk
