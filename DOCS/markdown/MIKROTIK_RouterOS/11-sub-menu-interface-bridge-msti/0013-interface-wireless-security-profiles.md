## `/interface wireless security-profiles` 

```
add authentication-types=wpa2-psk mode=dynamic-keys name=wlan_sec wpa2-pre-shared-key=use_a_long_password_here
/interface wireless
```

```
set wlan1 band=5ghz-a/n/ac channel-width=20/40/80mhz-Ceee disabled=no mode=station-bridge scan-list=5180
security-profile=wlan_sec ssid=ptp_test
```

**==> picture [13 x 13] intentionally omitted <==**

For each type of setup, there are different requirements, for PtP links NV2 wireless protocol is commonly used. You can read more about NV2 on the NV2 Manual page. 

When links are set up, you can enable bridge VLAN filtering on AP and ST : 

623 

```
/interface bridge
set bridge vlan-filtering=yes
```

**==> picture [13 x 13] intentionally omitted <==**

Double-check the bridge VLAN table before enabling VLAN filtering. A misconfigured bridge VLAN table can lead to the device being inaccessible and a configuration reset might be required. 

624
