## Configuring RouterOS device for 160MHz use 

If the RouterOS device supports 4x4 transmission, additionally to setting 160MHz channel width, make sure to set "rate-set=default" on the wireless interface so all streams are available 

If the client does not support Extended NSS and can only perform 2x2 transmission, set "vht-supported-mcs=mcs0-9,mcs0-9,none"
