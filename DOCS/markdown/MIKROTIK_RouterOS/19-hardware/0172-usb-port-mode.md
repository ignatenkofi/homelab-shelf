## USB Port Mode 

RB2011 series, CRS1xx series, and mAP have micro USB port which operates in host mode when USB device is attached through USB OTG cable. Some vendor cables require forced host mode to recognize connected device. 

Available properties: 

usb-mode (automatic | force-host; Default: "automatic") - Defines USB port mode. 

**==> picture [13 x 13] intentionally omitted <==**

Warning 

On RB2011 and CRS1xx series boards USB devices may not work first time they are plugged in. In such cases power cycle (not reboot) is required.
