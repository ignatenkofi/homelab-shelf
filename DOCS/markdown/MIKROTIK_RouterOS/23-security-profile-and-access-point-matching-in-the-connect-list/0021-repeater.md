## Repeater 

Wireless repeater will allow to receive the signal from the AP and repeat the signal using the same physical interface locally for connecting other clients. This will allow to extend the wireless service for the wireless clients. Wireless repeater function will configure the wireless interface to connect to the AP with station-bridge or station-pseudobridge option, create a virtual AP interface, create a bridge interface and add both (main and the virtual) interfaces to the bridge ports. 

If your AP supports button-enabled WPS mode, you can use the automatic setup command: 

```
/interface wireless setup-repeater wlan1
```

The setup-repeater does the following steps: 

searches for WPS AP with button pushed 

acquires SSID, key, channel from AP 

resets main master interface config (same as reset-configuration) 

- removes all bridge ports that were added for virtual interfaces added to this master (so there are no dangling invalid bridge ports later) removes all virtual interfaces added to this master 

- creates security profile with name "<interfacename>-<ssid>-repeater", if such security profile already exists does not create new, just updates settings 

- configures master interface, interface mode is selected like this: if AP supports bridge mode, use station-bridge, else if AP supports WDS, use station-wds, else use station-pseudobridge 

creates virtual AP interface with same SSID and security profile as master 

if master interface is not in some bridge, creates new bridge interface and adds master interface to it 

adds virtual AP interface to the same bridge master interface is in. 

If your AP does not support WPS , it is possible to specify the settings manually, using these parameters: 

address - MAC address of AP to setup repeater for (optional) 

ssid - SSID of AP to setup repeater for (optional) 

passphrase - key to use for AP - if this IS specified, command will just scan for AP and create security profile based on info in beacon and with this passphrase. If this IS NOT specified, command will do WPS to find out passphrase.
