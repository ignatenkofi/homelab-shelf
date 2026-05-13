## Compatibility and coexistence with other wireless protocols 

1503 

Nv2 protocol is not compatible to or based on any other available wireless protocols or implementations, either TDMA based or any other kind. This implies that only Nv2 supporting and enabled devices can participate in Nv2 network . 

Regular 802.11 devices will not recognize and will not be able to connect to Nv2 AP. RouterOS devices that have Nv2 support (that is - have RouterOS version 5.0rc1 or higher) will see Nv2 APs when issuing scan command, but will only connect to Nv2 AP if properly configured. 

As Nv2 does not use CSMA technology it may disturb any other network in the same channel. In the same way other networks may disturb Nv2 network, because every other signal is considered noise. 

The key points regarding compatibility and coexistence: 

- only RouterOS devices will be able to participate in Nv2 network 

- only RouterOS devices will see Nv2 AP when scanning 

- Nv2 network will disturb other networks in the same channel 

- Nv2 network may be affected by any (Nv2 or not) other networks in the same channel 

- Nv2 enabled device will not connect to any other TDMA based network
