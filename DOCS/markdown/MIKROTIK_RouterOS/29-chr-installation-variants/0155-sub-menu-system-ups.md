## Sub-menu: `/system ups` 

Standards: `APC Smart Protocol` 

The UPS monitor feature works with APC UPS units that support “smart” signalling over serial RS232 or USB connection. The UPS monitor service is not included in the default set of packages so it needs to be downloaded and installed manually with ups.npk package. This feature enables the network administrator to monitor the UPS and set the router to ‘gracefully’ handle any power outage with no corruption or damage to the router. The basic purpose of this feature is to ensure that the router will come back online after an extended power failure. To do this, the router will monitor the UPS and set itself to hibernate mode when the utility power is down and the UPS battery has less than 10% of its battery power left. The router will then continue to monitor the UPS (while in hibernate mode) and then restart itself when the utility power returns. If the UPS battery is drained and the router loses all power, the router will power back to full operation when the ‘utility’ power returns. 

The UPS monitor feature on the MikroTik RouterOS supports 

- hibernate and safe reboot on power and battery failure UPS battery test and run time calibration test 

- monitoring of all "smart" mode status information supported by UPS logging of power changes
