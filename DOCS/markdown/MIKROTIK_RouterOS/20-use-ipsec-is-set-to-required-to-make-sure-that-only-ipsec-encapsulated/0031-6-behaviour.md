## 6. Behaviour 

- Dynamic keys: Pulled from `/ip/ipsec/key/psk/` or QKD server, consumed once, then deleted. Static key: Configured per peer, used repeatedly. One-time dynamic keys ensure strongest protection but require synchronization. 

- Static fallback guarantees tunnel establishment but should be long enough (≥256 bits entropy). PPK usage can optionally be restricted to IKE SA only ( `psk-ike-initial` ) to reduce key consumption.
