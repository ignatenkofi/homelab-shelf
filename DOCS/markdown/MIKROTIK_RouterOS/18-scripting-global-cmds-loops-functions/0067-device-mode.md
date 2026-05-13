## Device-mode 

The device-mode is a feature which sets specific limitations on a device, or limits access to specific configuration options. Such feature is required in order to protect your router and network from attackers who might in some way gain access to your router and use it as a gateway for attacks to other networks. By protecting your device in such a way, even if an attacker manages to gain access to your unprotected device, he will not be able to use it in order to abuse your or any other network. 

There are three available modes: advanced, home and basic. Device modes are factory pre-installed to routers, if the router is manufactured and shipped with MikroTik RouterOS v7.17 or later. Advanced (previously called enterprise) mode is assigned to CCR and 1100 series devices, home mode is assigned to home routers and basic mode to any other type of device. For devices running versions prior to RouterOS version 7.17, all devices use the advanced /enterprise mode. 

```
[admin@MikroTik] > system/device-mode/print
                 mode: advanced
     allowed-versions: 7.13+,6.49.8+
              flagged: no
     flagging-enabled: yes
            scheduler: yes
                socks: yes
                fetch: yes
                 pptp: yes
                 l2tp: yes
       bandwidth-test: yes
          traffic-gen: no
              sniffer: yes
                ipsec: yes
                romon: yes
                proxy: yes
              hotspot: yes
                  smb: yes
                email: yes
             zerotier: yes
            container: no
  install-any-version: no
           partitions: no
          routerboard: yes
        attempt-count: 0
```

The device-mode can be changed by the user, but remote access to the device is not enough to change it. After changing the device-mode, you need to confirm it, by pressing a button on the device itself, or perform a "cold reboot" - that is, unplug the power. When the change is confirmed, regardless of confirmation mode, the device will be rebooted ! 

```
[admin@MikroTik] > system/device-mode/update mode=home
  update: please activate by turning power off or pressing reset or mode button
          in 5m00s
```

```
-- [Q quit|D dump|C-z pause]
```

If no power off or button press is performed within the specified time, the mode change is canceled. If another update command is run in parallel, both will be canceled. 

**==> picture [13 x 13] intentionally omitted <==**

There are several EOL products which do not "confirm" mode changes with a reset button press. These routers can confirm mode change only with a power cycle. 

In order to protect your device against attacker who might silently gain access to your router, abuse it with some scripts and simply try to wait until you will reboot your router and not even know that at that time you are accepting changes requested by some intruder, you can "update" mode only three times. There is a counter which will count how many update attempts are made and will not allow any more updates. This counter can be reset only when administrator does power-cycle the router or press a button when seeing such a warning on mode settings update attempt (same as with accepting any updates). 

```
[admin@MikroTik] > system/device-mode/update container=yes
  update: too many unsuccessful attempts, turn off power or reboot by pressing reset or mode button in 4m55s to
reset attempt-count
```

1131 

The following commands are available in the / system/device-mode menu: 

**==> picture [403 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>get Returns value that you can assign to variable or print on the screen.<br>print Shows the active mode and its properties.<br>update Applies changes to the specified properties, see below.<br>**----- End of picture text -----**<br>
