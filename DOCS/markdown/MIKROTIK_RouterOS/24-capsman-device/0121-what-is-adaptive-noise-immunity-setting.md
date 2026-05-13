## What is adaptive-noise-immunity setting? 

Adaptive Noise Immunity (ANI) adjusts various receiver parameters dynamically to minimize interference and noise effect on the signal quality. This setting is added in the wireless driver for Atheros AR5212 and newer chipset cards 

How does wireless device measure signal strength, when access-list or connect-list are used ? 

The reported signal level is exponentially weighted moving average with a smoothing factor of 50%. 

What error correction methods are supported in the RouterOS wireless? 

ARQ method is supported in nstreme protocols. Regular 802.11 standard does not include ARQ - retransmission of corrupt frames is based on acknowledgment protocol. RouterOS supports forward error correction coding (convolutional coding) with coding rates: 1/2, 2/3, or 3/4.
