## Configuration profiles 

One of the new WiFi additions is configuration profiles, you can create various presets, that can be assigned to interfaces as needed. Configuration settings for WiFi are grouped in profiles according to the parameter sections found at the end of this page - aaa , channel , configuration , datapath , interworki ng , and security , and can then be assigned to interfaces. Configuration profiles can include other profiles as well as separate parameters from other categories. 

This optional flexibility is meant to allow each user to arrange their configuration in a way that makes the most sense for them, but it also means that each parameter may have different values assigned to it in different sections of the configuration. 

The following priority determines, which value is used: 

1.  Value in interface settings 

2.  Value in a profile assigned to the interface 

3.  Value in configuration profile assigned to interface 

4.  Value in a profile assigned to the configuration profile (which in turn is assigned to the interface). 

If you are at any point unsure of which parameter value will be used for an interface, you can issue "/interface/wifi/print detail". The print command will show all values that the interface will have, including inherited values. 

To see only values that were configured directly on the interface, without displaying inherited ones, use "/interface/wifi/print config". 

For an example of configuration profile usage, see the following: 

1335 

Example for dual-band home AP `# Creating a security profile, which will be common for both interfaces /interface wifi security add name=common-auth authentication-types=wpa2-psk,wpa3-psk passphrase="diceware makes good passwords" wps=disable # Creating a common configuration profile and linking the security profile to it /interface wifi configuration add name=common-conf ssid=MikroTik country=Latvia security=common-auth # Creating separate channel configurations for each band /interface wifi channel add name=ch-2ghz frequency=2412,2432,2472 width=20mhz add name=ch-5ghz frequency=5180,5260,5500 width=20/40/80mhz # Assigning to each interface the common profile as well as band-specific channel profile, in case of "no supported channels" message on interfaces, make sure that correct (channel) configuration is applied to each. /interface wifi set wifi1 channel=ch-5ghz configuration=common-conf disabled=no set wifi2 channel=ch-2ghz configuration=common-conf disabled=no #"print detail" will show all values that interface will use, including inherited ones [admin@c52i] > interface/wifi/print detail Flags: M - master; D - dynamic; B - bound; X - disabled, I - inactive, R - running 0 M B  default-name="wifi1" name="wifi1" l2mtu=1560 mac-address=18:FD:74:AF:F4:28 arp-timeout=auto radiomac=18:FD:74:AF:F4:28 configuration=common-conf configuration.mode=ap .ssid="MikroTik" .country=Latvia security.authentication-types=wpa2-psk,wpa3-psk .passphrase="diceware makes good passwords" . wps=disable channel=ch-5ghz channel.frequency=5180,5260,5500 .width=20/40/80mhz 1 M B  default-name="wifi2" name="wifi2" l2mtu=1560 mac-address=18:FD:74:AF:F4:29 arp-timeout=auto radiomac=18:FD:74:AF:F4:29 configuration=common-conf configuration.mode=ap .ssid="MikroTik" .country=Latvia security.authentication-types=wpa2-psk,wpa3-psk .passphrase="diceware makes good passwords" . wps=disable channel=ch-2ghz channel.frequency=2412,2432,2472 .width=20mhz #using "print detail config" will show only the values that were directly configured on the interface [admin@c52i] > interface/wifi/print detail config Flags: M - master; D - dynamic; B - bound; X - disabled, I - inactive, R - running 0 M B  default-name="wifi1" name="wifi1" l2mtu=1560 mac-address=18:FD:74:AF:F4:28 arp-timeout=auto radiomac=18:FD:74:AF:F4:28 configuration=common-conf configuration.mode=ap channel=ch-5ghz 1 M B  default-name="wifi2" name="wifi2" l2mtu=1560 mac-address=18:FD:74:AF:F4:29 arp-timeout=auto radiomac=18:FD:74:AF:F4:29 configuration=common-conf configuration.mode=ap channel=ch-2ghz` 

**==> picture [13 x 12] intentionally omitted <==**

`print detail` and `print detail config` can also be used on `/interface/wifi/configuration` and will work in the same manner as in `/interface/wifi/` menu. 

Before 7.15 `/interface/wifi/actual-configuration/` menu was used, now the same functionality is achieved with the help of `print` command.
