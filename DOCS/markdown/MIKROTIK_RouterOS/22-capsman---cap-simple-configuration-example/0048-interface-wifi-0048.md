## `/interface wifi` 

```
set [ find default-name=wifi1 ] channel.frequency=5490 configuration.country=Latvia .mode=station .
ssid=input_your_SSID_here security.authentication-types=wpa2-psk .passphrase=input_your_password_here
```

`channel.frequency` → selects a frequency channel, which the AP uses. You can skip this, if you want to use "automatic" channel selection. `configuration.country` → applies the country profile, so that the device follows output power regulations. `.mode=station` → sets WiFi interface to operate in "station" mode. 

- `.ssid=input_your_SSID_here` → input the SSID name that the AP is broadcasting. 

`security.authentication-types=wpa2-psk` → specifies which authentication types to support. 

- `.passphrase=input_your_password_here` → set the password which AP expects. 

**==> picture [13 x 13] intentionally omitted <==**

There is a "distance" parameter that you have to configure additionally if your link is longer than 2km. This parameter does not work for `wifiqcom-ac` drivers. 

`configuration.distance=distance_in_km` → sets maximum link distance in kilometers. The value should reflect the distance to the AP or station that is furthest from the device. Unconfigured value allows usage of 2 km links.
