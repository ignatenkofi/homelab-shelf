## Instructions for Windows 

Download the Stable or Testing version of the Netinstall utility from the downloads page; Download the RouterOS Main package from the downloads page; 

**==> picture [13 x 13] intentionally omitted <==**

- You need to select a RouterOS version, preferably one marked as Stable . Additionally, choose the appropriate architecture (ARM, MIPS, SMIPS, TILE, etc.). If unsure, you can download the RouterOS package for all architectures, and Netinstall will determine the correct one for your device. 

Disable all computer network interfaces (WiFi, Ethernet, LTE, or any other type of connection) except for the one to be used for installation. Netinstall will only function with one active interface on your computer. It's strongly recommended to deactivate any other network interfaces to ensure Netinstall selects the correct one. 

Configure a static IP address for your Ethernet interface, open Start, and select Settings : 

85 

**==> picture [340 x 383] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

Netinstall can run also on a local network, in such case you could skip setting a static IP address, but it is highly recommended that you set a static IP address if you are not familiar with Netinstall. 

Open Network & Internet and select Change adapter options 

86 

**==> picture [450 x 356] intentionally omitted <==**

87 

**==> picture [452 x 356] intentionally omitted <==**

Right-click on your Ethernet interface and select Properties 

**==> picture [486 x 214] intentionally omitted <==**

Select Internet Protocol Version 4 (TCP/IPv4) and click Properties 

88 

**==> picture [273 x 352] intentionally omitted <==**

Check Use the following IP address and fill out the fields as shown in the image below 

89 

**==> picture [299 x 342] intentionally omitted <==**

Open your Downloads folder (or wherever you saved the downloaded files) and extract the Netinstall *.zip file to a convenient place 

90 

**==> picture [492 x 267] intentionally omitted <==**

**==> picture [384 x 284] intentionally omitted <==**

Make sure that the Ethernet interface is running and launch Netinstall.exe. If you followed the guide precisely, then you should not have any Internet connection on your computer, Windows 10 wants to verify all apps that it runs, but will not be able to do it since lack of an Internet connection, for this reason, a warning might pop up, you should click Run . 

**==> picture [13 x 13] intentionally omitted <==**

Netinstall requires administrator rights, there should be a window asking for permissions to run Netinstall, you must accept these permissions in order for Netinstall to work properly. 

Allow access for Netinstall in Public networks and configure Net booting settings and fill out the required fields as shown in the image below 

91 

**==> picture [380 x 276] intentionally omitted <==**

**==> picture [382 x 278] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

The Client IP address must be unique! Don't use an existing IP address in your network, this also means that you should not use the computer's IP address as well. Use a completely different IP address from the same subnet. 

Connect your device to your computer using an ethernet cable directly (without any other devices in-between), plug the Ethernet cable into your device's Etherboot port (see the next "Warning" in this article before connecting your Netinstll network). MikroTik devices are able to use Netinstall from their first port (Ether1), or from the port marked with " BOOT ". 

92 

**==> picture [277 x 141] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

Some computers have a network interface (especially USB Ethernet adapters) that tend to create an extra link flap, which is enough for Netinstall to fail to detect a device that is in Etherboot mode. In such a case you can use a switch between your device and your computer or a router in bridge mode to prevent this issue. If you use RouterOS powered router in bridge mode, then make sure that you disable any DHCP clients on the router bridge interface and disable Detect Internet feature. 

Netinstall uses bootp packets, which are using the same port numbers as DHCP packets. If you're using a switch between your PC and the device to be Netinstalled, ensure that the ports in the bridge are not blocked by other network devices. 

If you have dhcp-snooping enabled, make sure to enable "trusted" on the bridge ports facing the Netinstall PC. 

Power up your device and put it into etherboot mode 

**==> picture [13 x 13] intentionally omitted <==**

There are multiple ways how to put your device into Etherboot mode. Make sure you read the Etherboot manual before trying to put the device into this mode. Methods vary between different MikroTik devices. 

Wait for the device to show up in Netinstall, then select it and click Browse. Navigate to your Downloads folder (or wherever you saved your RouterOS packages) and press OK. 

93 

**==> picture [458 x 318] intentionally omitted <==**

**==> picture [226 x 247] intentionally omitted <==**

Select your desired RouterOS packages and press Install. Wait for the installation to finish and press " Reboot " (Devices without serial console have to be rebooted manually). 

**==> picture [13 x 13] intentionally omitted <==**

If you have downloaded RouterOS packages for multiple architectures, Netinstall will only display the appropriate architecture packages for your device after you have selected it. Unsupported packages will not appear in this window once a device is selected. 

94 

**==> picture [458 x 307] intentionally omitted <==**

**==> picture [458 x 307] intentionally omitted <==**

If the installation does not start (progress bar is not moving or no status is shown), then you can try closing the Netinstall application and opening it up again or try to put the device into Etherboot mode again. If you are still unable to get Netinstall working, then you should try using it on a different computer since there might be an operating system's issue that is preventing Netinstall from working properly. 

95 

**==> picture [13 x 13] intentionally omitted <==**

The "Keep old configuration" process involves downloading the configuration database from the router, reinstalling the router (including disk formatting), and uploading the configuration files back to it. However, it's important to note that this process solely applies to the configuration itself and does not impact the files, including databases like the User Manager database, Dude database, and others. 

After using Netinstall the device will be reset to defaults (unless you specified not to apply default configuration). Some devices are not accessible through e ther1 port with the default configuration for security reasons. Read more about Default configuration. 

Option "Keep branding" allows you to retain the device's already installed branding package without reinstalling it using Netinstall. 

**==> picture [458 x 307] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

When using the Configure script option, it is suggested to introduce a delay before configuration execution. 

You're all set! Configure your device and reconnect it to your network. Your device should now be functioning correctly!
