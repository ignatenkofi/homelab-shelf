## Access rule examples 

Only accept connections to guest network from nearby devices during business hours 

```
/interface/wifi/access-list/print detail
```

```
Flags: X - disabled
```

```
 0   signal-range=-60..0 allow-signal-out-of-range=5m ssid-regexp="MikroTik Guest" time=7h-19h days=mon,tue,wed,
thu,fri action=accept
```

```
 1   ssid-regexp="MikroTik Guest" action=reject
```

Reject connections from locally-administered ('anonymous'/'randomized') MAC addresses 

```
/interface/wifi/access-list/print detail
Flags: X - disabled
```

```
 0   mac-address=02:00:00:00:00:00 mac-address-mask=02:00:00:00:00:00 action=reject
```

Assigning a different passphrase for a specific client can be useful, if you need to provide wireless access to a client, but don't want to share your wireless password, or don't want to create a separate SSID. When the matching client connects to this network, instead of using the password defined in the interface configuration, the access list will make that client use a different password. Just make sure that the specific client doesn't get matched by a more generic access list rule first. 

Or reject all unknown MAC addresses, can be added as an ultimate rule, at the end of access list. - If you want to allow only specific clients on the network, make sure to also add a reject rule at the end of access-list, as there is no implicit reject rule by default.
