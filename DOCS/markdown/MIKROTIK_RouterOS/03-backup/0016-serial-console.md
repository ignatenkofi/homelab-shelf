## Serial console 

Some devices come with a serial console that can be used to put the device into Etherboot mode. To do so, make sure you configure your computer's serial console. The required parameters for all MikroTik devices (except for RouterBOARD 230 series) are as following: 

```
115200bit/s, 8 data bits, 1 stop bit, no parity, flow control=none by default.
```

For RouterBOARD 230 series devices the parameters are as following: 

```
9600bit/s, 8 data bits, 1 stop bit, no parity, hardware (RTS/CTS) flow control by default.
```

Make sure you are using a proper null modem cable, you can find the proper pinout here. When the device is booting up, keep pressing CTRL+E on your keyboard until the device shows that it is trying bootp protocol : 

99 

```
RouterBOOT booter 7.14.2
CRS328-4C-20S-4S+
CPU frequency: 800 MHz
  Memory size: 512 MiB
 Storage size:  16 MiB
Press Ctrl+E to enter etherboot mode
Press any key within 2 seconds to enter setup
trying bootp protocol.... OK
Got IP address: 192.168.88.3
resolved mac address 84:69:93:9E:E6:49
transfer started ............................... transfer ok, time=2.00s
```

At this point your device is in Etherboot mode, now the device should show up in your Netinstall window. 

100
