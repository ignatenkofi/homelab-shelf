## Available device-mode modes 

There are three device modes available for configuration (mode=advanced is default one), each mode has a subset of features that are not allowed when it is used. Note that there is no mode, which has all features enabled. Certain features need to be enabled even if you have "advanced" mode enabled. See section "Feature clarification" for more details about what each option means. So, as per the below table it can be seen that "traffic-gen, container, partitions, routerboard" features are always disabled, unless specifically enabled by the admin user. 

**==> picture [516 x 443] intentionally omitted <==**

**----- Start of picture text -----**<br>
Mode Description of disabled features<br>advanced (default - CCR and 1100  traffic-gen, container, install-any-version, partitions, routerboard<br>series devices)<br>basic  socks, bandwidth-test, traffic-gen, proxy, hotspot, zerotier, container, install-any-version, partitions, routerboard<br>home (home routers) scheduler, socks, fetch, bandwidth-test, traffic-gen, sniffer, romon, proxy, hotspot, email, zerotier, container, insta<br>ll-any-version, partitions, routerboard<br>List of available properties<br>Property Description<br>scheduler, socks, fetch, pptp, l2tp, bandwidth-test, traffic- The list of available features, which can be controlled with the  device-mode  option. See<br>gen, sniffer, ipsec, romon, proxy, hotspot, smb, email,  section "Feature clarification" for more details about what each option means.<br>zerotier, container, install-any-version, partitions,<br>routerboard   (yes | no)<br>activation-timeout  (default:  5m ); The reset button or power off activation timeout can be set in range 00:00:10 .. 1d00:00:00.<br>If the reset button is not pressed (or cold reboot is not performed) during this interval, the<br>update will be canceled.<br>flagging-enabled  (yes | no; Default: yes ) Device will perform configuration analysis and if traces of suspicious code are found, flagged<br>mode will be triggered, setting  flagged=yes , enabling restrictions described in the  flagged=yes<br>. See the See the "Flagged status" paragraph.<br>flagged  (yes | no; Default: no ) RouterOS employs various mechanisms to detect tampering with it's system files. If the<br>system has detected unauthorized access to RouterOS, the status "flagged" is set to yes. If<br>"flagged" is set to yes, for your safety, certain limitations are put in place. See below chapter<br>for more information.<br>mode:  (basic, home, advanced; default:  advanced ); Allows choosing from available modes that will limit device functionality.<br>By default,  advanced  mode allows options except  traffic-gen, container, partitions, install-<br>any-version, routerboard.  So to use these features, you will need to turn it on by performing<br>a device-mode update.<br>By default,  home  mode disables the following features:  scheduler, socks, fetch, bandwidth-<br>test, traffic-gen, sniffer, romon, proxy, hotspot, email, zerotier, container, install-any-version,<br>partitions, routerboard.<br>**----- End of picture text -----**<br>

More specific control over the available features is possible. Each of the features controlled by device-mode can be specifically turned on or off. 

For instance scheduler won't allow to perform any action at system scheduler. Used device-mode disables all listed features, for instance mode =home is used, but zerotier is required for your setup, device-mode update /system device-mode update zerotier=yes will be required with the physical access to device to push the button or cut the power. 

1132 

```
[admin@MikroTik] > system/device-mode/update mode=home email=yes
[admin@MikroTik] > system/device-mode/update mode=advanced zerotier=no
```

If the update command specifies any of the mode parameters, this update replaces the entire device-mode configuration. In this case, all "per-feature" settings will be lost, except those specified with this command. For instance: 

```
[admin@MikroTik] > system/device-mode/update mode=home email=yes fetch=yes
[admin@MikroTik] > system/device-mode/print config
   mode: home
  fetch: yes
  email: yes
[admin@MikroTik] > system/device-mode/update mode=advanced sniffer=no
-- reboot --
[admin@MikroTik] > system/device-mode/print config
     mode: advanced
  sniffer: no
```

We see that fetch = yes and email = yes is missing, as they were overriden with the mode change. However, specifying only "per-feature" settings will change only those: 

```
[admin@MikroTik] > system/device-mode/update hotspot=no
-- reboot --
[admin@MikroTik] > system/device-mode/print config
     mode: advanced
  sniffer: no
  hotspot: no
```

If the feature is disabled, an error message is displayed for interactive commands: 

```
[admin@MikroTik] > system/device-mode/print config
     mode: advanced
  sniffer: no
  hotspot: no
[admin@MikroTik] > tool/sniffer/quick
failure: not allowed by device-mode
```

However, it is possible to add the configuration to a disabled feature, but there will be a comment showing the disabled feature in the device-mode: 

```
[admin@MikroTik] > ip hotspot/add interface=ether1
[admin@MikroTik] > ip hotspot/print
Flags: X, S - HTTPS
Columns: NAME, INTERFACE, PROFILE, IDLE-TIMEOUT
#   NAME      INTERFACE  PROFILE  IDLE-TIMEOUT
;;; inactivated, not allowed by device-mode
0 X hotspot1  ether1     default  5m
```
