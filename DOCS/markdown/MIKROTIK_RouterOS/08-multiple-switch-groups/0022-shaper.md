## Shaper 

Traffic shaping restricts the rate and burst size of the flow which is transmitted out from the interface. The shaper is implemented by a token bucket. If the packet exceeds the maximum rate or the burst size, which means not enough token for the packet, the packet is stored to buffer until there is enough token to transmit it.
