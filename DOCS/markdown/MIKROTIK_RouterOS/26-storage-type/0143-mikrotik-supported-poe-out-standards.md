## MikroTik supported PoE-Out standards 

MikroTik devices can support some or all of the following PoE standards: 

1727 

- Passive PoE-Out up to 30 V - PoE standard, which does not require negotiation between PSE (Power Sourcing Equipment) and PD (Powered Device). PoE-out uses the same voltage as supplied to the PSE (Power Sourcing Equipment). PoE-Out Standard for devices that supports input voltage up to 30 V. (e.g. hEX PoE lite, RB3011UiAS-RM, RB2011iL-IN.) 

- Passive PoE-Out up to 57 V - Works the same as low voltage (up to 30 V) PoE-Out, but is also capable to deliver high voltage over PoE ports. The output voltage depends on the power source connected to PSE. Can power up af/at compatible devices, which accepts power over 4,5 (+) and 7,8 (-), and does not require PoE negotiation. (e.g. cAP ac, hAP ac, wsAP ac lite.) 

- IEEE Standards 802.3af/at - Also known as PoE+ Type 1 (af) and PoE+ Type 2 (at), these IEEE standards aim to ensure compatibility between vendors. MikroTik PSEs that support these standards can power both Type 1 and Type 2 PDs. MikroTik devices that support af/at standard can also power devices that accept Passive PoE-In. (e.g. CRS112-8P-4S-IN, CRS328-24P-4S+RM, CRS354-48P-4S+2Q+RM.) 

- IEEE Standards 802.3bt -  The 802.3bt standard, also known as PoE++, extends the earlier PoE standards and introduces "Type 3" (Classes 5-6) and "Type 4" (Classes 7-8). This standard uses all four pairs of wires in Gigabit Ethernet cable to deliver power, hence the name of the standard - 4PPoE/802.3bt ("4-pair Power over Ethernet"). 802.3bt powering is isolated from PoE-Out and the device powering itself. (e.g CRS320-8P-8B4S+RM) 

Each PoE-Out implementation supports overload and short-circuit detection.
