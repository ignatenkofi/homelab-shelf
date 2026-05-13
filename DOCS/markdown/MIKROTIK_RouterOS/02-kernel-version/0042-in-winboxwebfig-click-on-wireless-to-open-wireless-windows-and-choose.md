## in Winbox/Webfig click on Wireless to open wireless windows and choose the Security Profile tab. 

**==> picture [504 x 282] intentionally omitted <==**

If there are legacy devices that do not support WPA2 (like Windows XP), you may also want to allow WPA protocol. 

**==> picture [13 x 13] intentionally omitted <==**

WPA and WPA2 pre-shared keys should not be the same. 

Now when the security profile is ready we can enable the wireless interface and set the desired parameters 

```
/interface wireless
```

```
  enable wlan1;
```

```
  set wlan1 band=2ghz-b/g/n channel-width=20/40mhz-Ce distance=indoors \
    mode=ap-bridge ssid=MikroTik-006360 wireless-protocol=802.11 \
    security-profile=myProfile frequency-mode=regulatory-domain \
    set country=latvia antenna-gain=3
```

To do the same from WinBox/WebFig: 

Open Wireless window, select wlan1 interface, and click on the enable button; Double click on the wireless interface to open the configuration dialog; 

- In the configuration dialog click on the Wireless tab and click the Advanced mode button on the right side. When you click on the button additional configuration parameters will appear and the description of the button will change to Simple mode ; Choose parameters as shown in the screenshot, except for the country settings and SSID. You may want to also choose a different frequency and antenna gain; 

31 

Next, click on the HT tab and make sure both chains are selected; Click on the OK button to apply settings. 

**==> picture [504 x 302] intentionally omitted <==**

The last step is to add a wireless interface to a local bridge, otherwise connected clients will not get an IP address: 

```
/interface bridge port
  add interface=wlan1 bridge=bridge1
```

Now wireless should be able to connect to your access point, get an IP address, and access the internet.
