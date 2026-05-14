## Serial Terminal Usage 

RouterOS allows to communicate with devices and other systems that are connected to the router via the serial port using a `/system serialterminal` command. All keyboard input will be forwarded to the serial port and all data from the port is output to the connected device. 

First, you have to have a free serial port, if the device has only one serial port (like all RouterBoards, WRAP/ALIX boards, etc.) you will have to disable the system console on this serial port to be able to use it as Serial Terminal for connection to other equipment (switches, modems, etc): 

```
/system console disable 0
```

Be sure to just disable the console rather than removing it, as RouterOS will recreate the console after the next reboot when you really remove it. 

239 

**==> picture [13 x 13] intentionally omitted <==**

Note that there are some caveats you should be aware of! Take your time understanding those limits to avoid strange things to happen when connecting a device to a serial port on a RouterBoard: 

By re-configuring port Serial0 on a RouterBoard as seen above, you will lose your serial console access to RouterOS. This means, that if you cannot access your RouterBoard over the network anymore, you might even have to reset the whole configuration of it to gain access again. 

When rebooting a RouterBoard the boot loader (RouterBOOT) will always use the serial console (Serial0 on RouterBoards) to send out some startup messages and offer access to the RouterBOOT menu. 

Having text coming out of the serial port to the connected device might confuse your attached device. Furthermore, in the standard config, you can enter the RouterBOOT menu by pressing ANY key. So if your serial device sends any character to the serial port of your RouterBoard during boot time, the RouterBoard will enter the RouterBOOT menu and will NOT boot RouterOS unless you manually intervene! 

You can reconfigure RouterBOOT to enter the RouterBOOT menu only when a DEL character is received - use this to reduce the chance to get a router that's stuck when rebooting! 

Or if newer versions are used "Silent boot" feature can be used to suppress any output on the serial interface, including removal of booting sounds. 

Next, you will have to configure your serial port according to the serial port settings of the connected device. Using the following command you will set your serial port to 19200 Baud 8N1. What settings you need to use depends on the device you connect: 

```
/port set serial0 baud-rate=19200 data-bits=8 parity=none stop-bits=1
```

You can also try to let RouterOS guess the needed baud rate by setting 

```
/port set serial0 baud-rate=auto
```

Now's the time to connect your device if not already done. Usually, you will have to use a null modem cable (the same thing as a cross-over-cable for Ethernet). Now we're ready to go: 

```
/system serial-terminal serial0
```

This will give you access to the device you connected to port Serial0. Ctrl-A is the prefix key, which means that you will enter a small "menu". If you need to send the Ctrl-A character to a remote device, press Ctrl-A twice. 

If you want to exit the connection to the serial device type Ctrl-A , then . This will return you to your RouterOS console. Q 

**==> picture [13 x 13] intentionally omitted <==**

Do not connect to devices at an incorrect speed and avoid dumping binary data.
