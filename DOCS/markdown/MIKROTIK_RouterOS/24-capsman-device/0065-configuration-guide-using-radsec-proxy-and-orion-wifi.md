## Configuration guide using RadSec proxy and Orion Wifi: 

This guide describes how to set up your MikroTik devices so you can use them with RadSec proxy and Orion Wifi, though the main configuration steps remain the same and will work with different providers as well: 

This guide assumes that you have configured a radsecproxy with Orion Wifi credentials. Make sure to use the latest long-term or stable RouterOS releases. 

It is important to set up a secure RADIUS connection between the wireless LAN controller and Orion Wifi. 

Orion Wifi uses RADIUS over TLS (RadSec) to ensure end-to-end encryption of AAA traffic. This guide is made for scenarios where the RouterOS access point redirects AAA traffic to a RadSec proxy (radsecproxy) before the traffic is sent over the internet. 

1) Configure the Radius client that points to radsecproxy. 

1520 

**==> picture [505 x 266] intentionally omitted <==**

Command line equivalent is “/radius add address=192.168.88.233 secret=yourSecret service=wireless timeout=1s500ms” The secret should match the one configured on the radsecproxy, in this example “192.168.88.233” is a virtual machine running the proxy. 

- 2) Create a wireless security profile that would perform 802.1x authentication 

1521 

**==> picture [505 x 361] intentionally omitted <==**

**==> picture [387 x 193] intentionally omitted <==**

1522 

**==> picture [386 x 143] intentionally omitted <==**

Command line equivalent is “/interface wireless security-profiles add authentication-types=wpa2-eap management-protection=allowed mode=dynamickeys name=dot1x_profile supplicant-identity="" radius-eap-accounting=yes eap-methods=passthrough“. 

3) The next step is configuring the wireless interface and assigning the created security profile. Press “Advanced mode” to see all the options. 

1523 

**==> picture [397 x 485] intentionally omitted <==**

Command line equivalent is: "/interface wireless set [ find default-name=wlan1 ] mode=ap-bridge security-profile=dot1x_profile wps-mode=disabled". 

Make sure the correct country profile is configured. In this example, we are using “wlan1”, but the same command would work with other interfaces, or as “/i nterface wireless set wlan1”. 

- 4) Configure interworking settings (hotspot 2.0 ). 

1524 

**==> picture [505 x 189] intentionally omitted <==**

**==> picture [505 x 348] intentionally omitted <==**

1525 

**==> picture [505 x 307] intentionally omitted <==**

Command line equivalent: “/interface wireless interworking-profile add domain-names=orion.area120.com ipv4-availability=public name=Orion_MikroTik network-type=public-chargeable operator-names=Orion:eng realms=orion.area120.com:eap-tls roaming-ois=f4f5e8f5f4,baa2D00100,baa2d00000 venue=business-unspecified venue-names=Orion:eng wan-downlink=50 wan-uplink=50 wan-status=up”. 

**==> picture [13 x 13] intentionally omitted <==**

Be sure to specify somevalue in "wan-downlink" and "wan-uplink", in this scenario value of "50" is used as a placeholder, some client devices use it to evaluate, if they should join the network. Set “venue” – venue type, ”venue-names” and other attributes as applicable. “domain-names” should be of hotspot 2.0 Operator. 

5) Assign the interworking profile to the interface. 

1526 

**==> picture [505 x 260] intentionally omitted <==**

This step can also be done with the following command: “/interface wireless set wlan1 interworking-profile=Orion_MikroTik”. 

If the radsecproxy is working, then clients with the appropriate Hotspot profile installed should be able to connect. 

Note: NAS-id that's used by Orion to differentiate networks is equal to system identity, to adjust the nas-id, you can do "/system identity set name=exampleName". Graphical interface support for interworking profiles is added from versions above 6.47.10, 6.48.3.
