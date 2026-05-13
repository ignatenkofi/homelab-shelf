## Sub-menu: `/system watchdog` 

This menu allows the configuring system to reboot, when a specific IP address does not respond, or when it detects, that the software has locked up. The detection is done in two ways: 

Software watchdog timer (mostly caused by hardware malfunction) device can recover itself with a reboot; Ping watchdog can monitor connectivity to a specific IP address and trigger the reboot function. 

**==> picture [13 x 13] intentionally omitted <==**

Note: These are two different Watchdog features and both have their own settings. By default software Watchdog is enabled and ping Watchdog is disabled. You can enable ping Watchdog by specifying an IP address and you can disable the software Watchdog by unsetting the Watchdog Timer option. 

**==> picture [13 x 13] intentionally omitted <==**

Note: Watchdog reboot is not a system failure. Such reboot also will not generate autosupout file. Watchdog reboot is "/system reboot" automatically triggered by operating system when some service is not responding as fast as it should. Reasons for that can vary between damaged hardware, slow software implementation for some service, DDoS attack, bad configuration and others.
