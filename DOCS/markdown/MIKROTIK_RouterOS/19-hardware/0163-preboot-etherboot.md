## Preboot etherboot 

preboot-etherboot is a feature that instructs RouterOS device to search for a Netinstall server on every boot for specified amount of time, before starting the regular booting process (e.g., RouterOS). This feature is particularly useful for remote reinstall, as it allows the device to attempt etherboot on every startup. 

preboot-etherboot-server specifies that the preboot-etherboot booter should look only for a Netinstall server with a specific IP address. Since by default, etherboot accepts address from any BOOTP/DHCP server,  with this feature, you can specify to accept the address only from a particular Netinstall server, meaning that the device can be reinstalled without removing it from the network. 

With both features enabled, any device can be reinstalled remotely without accessing RouterOS or holding the reset button. One example of starting a remote reinstall process would be to simply power cycle RouterOS device from a PoE switch or another power controller. After installation, disable your Netinstall server and simply power cycle the installed device. 

To enable preboot-etherboot and preboot-etherboot-server : 

1) Install RouterOS version 7.9+ 

2) Upgrade RouterBOOT with "/system routerboard upgrade" 

3) Reboot 

The feature can be set with command: 

1747 

```
system/routerboard/settings/set preboot-etherboot=9s preboot-etherboot-server=10.155.115.199
```

On every next reboot/power cycle, this device will try to receive IP address from Netinstall server with IP 10.155.115.199, for 9 seconds. If there will be no such server, regular boot process will start. 

**==> picture [13 x 13] intentionally omitted <==**

In case if the preboot-etherboot is set to boot from any IP (preboot-etherboot-server is not specified), the device will enter etherboot mode from any Netinstall/DHCP server-provided IP address and will wait for the reinstall process. Also, note that RouterOS reinstall does not affect BIOS settings, and preboot-etherboot would still be enabled and would try to enter etherboot. To avoid this scenario without accessing RouterOS, simply disable any attached Netinstall/DHCP server.
