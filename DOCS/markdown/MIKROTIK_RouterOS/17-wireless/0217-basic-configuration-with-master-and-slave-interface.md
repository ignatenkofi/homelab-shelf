## Basic configuration with master and slave interface 

Create security profile for WPA2 PSK, without specifying passphrase: 

```
[admin@CM] /caps-man security>add name="wpa2psk" authentication-types=wpa2-psk encryption=aes-ccm
```

Create configuration profile to be used by master interface 

specify WPA2 passphrase in configuration specify channel settings in configuration: 

```
[admin@CM] /caps-man configuration> add name=master-cfg ssid=master security=wpa2psk
security.passphrase=12345678 channel.frequency=5180 channel.width=20 channel.band=5ghz-a
```

Create configuration profile to be used by virtual AP interface 

specify different WPA2 passphrase in configuration: 

```
[admin@CM] /caps-man configuration> add name=slave-cfg ssid=slave security=wpa2psk
security.passphrase=87654321
```

Create provisioning rule that matches any radio and creates dynamic interfaces using master-cfg and slave-cfg: 

```
[admin@CM] /caps-man provisioning> add action=create-dynamic-enabled master-configuration=master-cfg
slave-configurations=slave-cfg
```

Now when AP connects and is provisioned 2 dynamic interfaces (one master and one slave) will get created: 

1487 

```
[admin@CM] /caps-man interface> print detail
Flags: M - master, D - dynamic, B - bound, X - disabled, I - inactive, R - running
0 MDB  name="cap1" mtu=1500 l2mtu=2300 radio-mac=00:0C:42:1B:4E:F5 master-interface=none
       configuration=master-cfg
```

```
1  DB  name="cap2" mtu=1500 l2mtu=2300 radio-mac=00:00:00:00:00:00 master-interface=cap1
       configuration=slave-cfg
```

Consider an AP, that does not support configured frequency connects and can not become operational: 

```
[admin@CM] /caps-man interface> pr
Flags: M - master, D - dynamic, B - bound, X - disabled, I - inactive, R - running
#      NAME                                 RADIO-MAC         MASTER-INTERFACE
0 MDB  ;;; unsupported band or channel
       cap3                                 00:0C:42:1B:4E:FF none
...
```

We can override channel settings for this particular radio in interface settings, without affecting master-cfg profile: 

```
[admin@CM] /caps-man interface> set cap3 channel.frequency=2142 channel.band=2ghz-b/g
```

Allow Specific MAC address range to match the Access-list, for example, match all the Apple devices: 

```
[admin@CM] /caps-man access-list> add mac-address=18:34:51:00:00:00 mac-address-mask=FF:FF:FF:00:00:00
action=accept
```

Configuring DHCP Server Option 138 for setting the CAPsMAN address on the CAP boards 

```
[admin@CM] /ip dhcp-server network set <network-id> caps-manager=<capsman-server-ip>
```

DHCP client this CAPsMAN IP will see in "/ip dhcp-client print detail"
