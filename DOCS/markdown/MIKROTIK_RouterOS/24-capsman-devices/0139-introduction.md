## Introduction 

The spectral scan can scan all frequencies supported by your wireless card, and plot them directly in the console. The exact frequency span depends on the card. Allowed ranges on r52n: [4790; 6085], [2182; 2549]. 

A wireless card can generate 4us long spectral snapshots for any 20mhz wide channel. This is considered a single spectral sample. 

To improve data quality spectrum is scanned with 10mhz frequency increments, which means doubled sample coverage at each specific frequency (considering 20mhz wide samples). 

**==> picture [13 x 12] intentionally omitted <==**

Currently, is NOT supported for Atheros 802.11ac chips (e.g. QCA98xx, IPQ-4018). See https://mikrotik.com/products determine the wireless chip on your device.
