## `/interface wifi` 

```
set [ find default-name=wifi1 ] channel.frequency=5490 configuration.country=Latvia .mode=ap .
```

```
ssid=input_your_SSID_here security.authentication-types=wpa2-psk .passphrase=input_your_password_here .
width=20mhz
```

`channel.frequency` → selects a frequency channel on which to run the AP. You can skip this, if you want to use "automatic" channel selection. `configuration.country` → applies the country profile, so that the device follows output power regulations. 

`.mode=ap` → sets WiFi interface to operate in "access point" mode. 

`.ssid=input_your_SSID_here` → configures the SSID name the AP is going to broadcast. 

`security.authentication-types=wpa2-psk` → specifies which authentication types to support. 

`.passphrase=input_your_password_here` → sets password for the SSID. 

**==> picture [13 x 13] intentionally omitted <==**

There is a "distance" parameter that you have to configure additionally if your link is longer than 2km. This parameter does not work for `wifiqcom-ac` drivers. 

`configuration.distance=distance_in_km` → sets maximum link distance in kilometers. The value should reflect the distance to the AP or station that is furthest from the device. Unconfigured value allows usage of 2 km links. 

`.width=20mhz` → set channel width. The lower the width of the channel, the longer the distance (less interference).
