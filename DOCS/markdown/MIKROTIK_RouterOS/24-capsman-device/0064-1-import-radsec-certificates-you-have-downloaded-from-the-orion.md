## 1) Import RadSec certificates you have downloaded from the Orion: 

Drag and drop certificate in WinBox, and then use the import function for it, which can be found under /system certificates in WinBox, command line equivalent is :"/certificate import file-name=bw.radsec.cacert.pem passphrase=""", "/certificate import file-name=cert.pem passphrase=""", "/certificate import file-name=key.pem passphrase=""" 

**==> picture [505 x 274] intentionally omitted <==**

1513 

**==> picture [264 x 170] intentionally omitted <==**

**==> picture [264 x 175] intentionally omitted <==**

Once certificates are imported, they should look like this: 

**==> picture [203 x 96] intentionally omitted <==**

2) Configure the Radius client 

1514 

**==> picture [505 x 279] intentionally omitted <==**

Command line equivalent: "/radius add address=216.239.32.91 certificate=cert.pem_0 protocol=radsec service=wireless timeout=1s500ms" 

3)  Create a wireless security profile that would perform 802.1x authentication 

**==> picture [505 x 361] intentionally omitted <==**

1515 

**==> picture [387 x 194] intentionally omitted <==**

**==> picture [386 x 144] intentionally omitted <==**

Command line equivalent is “/interface wireless security-profiles add authentication-types=wpa2-eap management-protection=allowed mode=dynamickeys name=dot1x_profile supplicant-identity="" radius-eap-accounting=yes eap-methods=passthrough“. 

4) The next step is configuring the wireless interface and assigning the created security profile. Press “Advanced mode” to see all the options. 

1516 

**==> picture [397 x 485] intentionally omitted <==**

Command line equivalent is: "/interface wireless set [ find default-name=wlan1 ] mode=ap-bridge security-profile=dot1x_profile wps-mode=disabled". 

Make sure the correct country profile is configured. In this example, we are using “wlan1”, but the same command would work with other interfaces, or as “/i nterface wireless set wlan1”. 

- 5) Configure interworking settings (hotspot 2.0 ). 

1517 

**==> picture [505 x 189] intentionally omitted <==**

**==> picture [505 x 348] intentionally omitted <==**

1518 

**==> picture [505 x 307] intentionally omitted <==**

Command line equivalent: “/interface wireless interworking-profile add domain-names=orion.area120.com ipv4-availability=public name=Orion_MikroTik network-type=public-chargeable operator-names=Orion:eng realms=orion.area120.com:eap-tls roaming-ois=f4f5e8f5f4,baa2D00100,baa2d00000 venue=business-unspecified venue-names=Orion:eng wan-downlink=50 wan-uplink=50 wan-status=up”. 

**==> picture [13 x 13] intentionally omitted <==**

Pay special attention to "wan-downlink" and "wan-uplink", in this scenario value of "50" is used as a placeholder, make sure to adjust the values according to your setup, some client devices use it to evaluate, if they should join the network. Set “venue” – venue type, ”venue-names” and other attributes as applicable. “domain-names” should be of hotspot 2.0 Operator. 

6) Assign the interworking profile to the interface. 

1519 

**==> picture [505 x 260] intentionally omitted <==**

Command-line equivalent is: “/interface wireless set wlan1 interworking-profile=Orion_MikroTik”. If you don't see the interworking-profile field, press "Advanced mode". 

Note: NAS-id that's used by Orion to differentiate networks is equal to system identity, to adjust the nas-id, you can do "/system identity set name=exampleName". Graphical interface support for interworking profiles are added from versions above 6.47.10, 6.48.3.
