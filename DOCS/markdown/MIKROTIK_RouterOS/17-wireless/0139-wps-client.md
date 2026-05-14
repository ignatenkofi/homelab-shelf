## WPS Client 

WPS Client function allows the wireless client to get the Pre-Shared Key configuration of the AP that has WPS Server enabled. WPS Client can be enabled by such command: 

```
 /interface wireless wps-client wlan1
```

WPS Client command outputs all the information of the WPS Enabled AP on the screen. Example: 

```
[admin@MikroTik] /interface wireless> wps-client wlan1
          status: disconnected, success
            ssid: MikroTik
     mac-address: E4:8D:8C:D6:E0:AC
      passphrase: presharedkey
  authentication: wpa2-psk
      encryption: aes-ccm
```

It is possible to specify additional settings for the WPS-Client command: 

1424 

- create-profile - creates wireless security profile with the specified name, configures it with security details received from the WPS AP, specifies the wireless interface to use the new created security profile 

ssid - get WPS information only from AP with specified SSID 

mac-address - get WPS information only from AP with specified mac-address
