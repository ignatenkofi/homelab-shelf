## Troubleshooting 

In cases where a PD does not power-up or reboots unexpectedly when powered from your PSE, it's suggested to the first check: 

1735 

PD supported input voltage - PSE output voltage must be in the range supported by the PD. Otherwise, the PD is incompatible with the PSE, and will not be able to power-up. Check the PD datasheet. 

PD supported input PoE-in standard - Some PDs do not support af/at standard even if it has PoE-in support up to 57 V, check PD datasheet. PD is rebooted from PSE 

Check if PD does not exceed PoE-Out port limit and Total-PoE-Out port limit of the PSE, check PSE datasheet. 

Check if the Voltage limit does not drop bellow supported (Can be caused by voltage drop on the wires). 

Check if you are using a proper power supply, the output power of PSU should be calculated from: 

- `(MAX power consumption of PSE) + (MAX power consumption of all PD) + 10%)` 

Check if you are using good quality ethernet cables, it's important especially in cases if PoE is used. 

Check RouterOS version - it's possible, that some PoE related features will be updated with RouterOS, make sure that you are running the latest RouterOS version. 

PD Does not power up 

There can be cases where a PD does not power up, even though it supports passive PoE, and does not consume more power than the specified PSE port limit. This can be caused by inrush current triggering overcurrent protection on the PSE. Make sure that PD specification supports powering from PSE (not only from passive power injector) 

Polarity - Devices with opposite or different pinouts can be unable to powerup from all PSE. Check the PD datasheet. 

Incompatible resistance - PD resistance should have ranged from 3kΩ to 26.5kΩ (For Passive-PoE) and from 23.75kΩ to 26.25kΩ on af /at.
