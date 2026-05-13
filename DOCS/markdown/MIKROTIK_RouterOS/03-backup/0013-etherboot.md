## Etherboot 

Etherboot mode is a special state for a MikroTik device that allows you to reinstall your device using Netinstall. There are two types of booters available for use: the regular booter and the backup booter. It's essential to verify both options. 

- To use the Regular booter press Ctrl+E to enter etherboot mode using the serial console or press the Reset button after a 1-2 second delay from when you power it on. 

- To employ the backup booter, power OFF the device. Press the Reset button and power on your device (wait until the "USR" led is blinking then stable "On", and when the "USR" led is "Off" - release the Reset button) - the device is booting in bootp mode to reinstall RouterOS using Netinstall.
