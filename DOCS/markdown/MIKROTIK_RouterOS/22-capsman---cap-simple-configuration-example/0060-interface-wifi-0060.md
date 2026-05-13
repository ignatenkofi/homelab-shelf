## `/interface wifi` 

```
set [ find default-name=wifi2 ] configuration.mode=station-bridge .ssid=router.ssid.2 disabled=no security.
authentication-types=wpa2-psk .passphrase=router.password
```

`configuration.mode=station-bridge` → selects the station mode. 

**==> picture [13 x 13] intentionally omitted <==**

Which station mode to use? 

For MikroTik Wi-Fi 6 AX (router that uses `wifi-qcom` package/drivers) to MikroTik Wi-Fi 6 AX (repeater/station that uses `wifi-qcom` package /drivers) connection, use **`station-bridge`** mode. 

For 3d-party-vendor or MikroTik legacy WiFi 5 AC and below (router) to Wi-Fi 6 AX (repeater) connection, use **`station-pseudobridge`** mode. 

`station-pseudobridge` does something similar to "Network Address Translation" but with MAC addresses. With this mode, if you have multiple devices connected to the repeater and they all access the internet, the router would see all those attempts coming from a single MAC address. Basically, all client devices would be hidden behind one MAC address, which could potentially cause networking issues. It is not advised to use this mode, but, in such cases, there are no other options. 

- `configuration.country=Latvia` → select your actual country, so that you do not break any regulations (your country "laws"). Different country profiles have different allowed output powers per different frequency ranges. 

- `ssid=router.ssid.2` → it is the 2.4 GHz SSID network name that the router broadcasts (where the repeater should connect). `security.authentication-types=wpa2-psk` → selects, which authentication types the main router uses. 

- `passphrase=router.password` → configures the password from the main router network. The password configured in your router's settings.
