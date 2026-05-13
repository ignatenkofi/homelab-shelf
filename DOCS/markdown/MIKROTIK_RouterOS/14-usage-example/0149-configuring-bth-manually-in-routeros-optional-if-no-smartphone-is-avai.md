## Configuring BTH manually in RouterOS (optional, if no smartphone is available to you) 

**==> picture [13 x 13] intentionally omitted <==**

Important notice 

It is important to note, NOTHING has to be configured in RouterOS to use Back to Home . Simply use the BTH app (see above section) to enable it. The whole point of Back to Home is to avoid using Winbox or command line. Below instructions are only for debugging or seasoned administrators. 

1.  Connect to router 

875 

2.  Enable DDNS Cloud service:  /ip/cloud/set ddns-enabled=yes` ` 

3.  Enable Back To Home:  /ip/cloud/set back-to-home-vpn=enabled` ` 

4.  Print tunnel configuration:  /ip/cloud/print` ` 

5.  Scan QR Code ( vpn-wireguard-client-config-qrcode` `) or Copy config ( vpn-wireguard-client-config` `) and enter in preferred 

WireGuard® client. Only one client at a time will be available to use this config. 

**==> picture [13 x 13] intentionally omitted <==**

After configuring Back To Home - an additional peer entry is automatically made, which can be seen by running the command /ip cloud print. This is intended for the VPN to work in the case that the device does not have access to a public IP address and opts to establish the connection by using MikroTIk's relay server. 

In the case your device has access to a public IP address, the generated peer entry is ignored: 

```
[Peer]
PublicKey = //////////////////////////////////////////8=
AllowedIPs = 0.0.0.0/32
Endpoint = example.com:12345
PersistentKeepalive = 15
```
