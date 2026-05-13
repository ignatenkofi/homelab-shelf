## Point to Multi Point setup example 

All MikroTik devices can be interconnected. There are three different versions of wAP60G devices currently available: 

Wireless Wire kit wAP 60G SXTsq60 Lite60 wAP 60G AP 

1429 

And 

Wireless Wire Dish 

Hardware wise wAP devices are identical, but there are some software limitations - 

wAP 60G AP is designed for Access Point usage in PtMP (Point to Multi Point) setups, but can be also used as PtP (Point to Point) or as Station device. It's already equipped with level4 license for more than one connected client support More about Licenses 

Wireless Wire kit , Wireless Wire Dish , SXTsq Lite60 and wAP60G devices comes with level3 license. Wireless wire dish should be only used as Client device due to it's narrow radiation pattern. 

License upgrade is needed to unlock more than one simultaneously connected client in Access Point mode, but devices can connect to Access Points as regular Station devices. 

**==> picture [13 x 13] intentionally omitted <==**

Before configuration, make sure devices are running latest software versions: How to upgrade 

Minimal configuration for transparent wireless link is matching SSID, correct mode (bridge || station-bridge) and Wireless and Ethernet interfaces put in same bridge. 

In current example we will look at usage case where wAP60G AP is used as Access Point, wAP60G and Wireless Wire kit devices are used as Station devices, forming 4 unit network. 

**==> picture [13 x 13] intentionally omitted <==**

It's recommended to change default IP addresses to avoid connection issues to the devices 

wAP60G AP units come pre-configured with WISP Bridge default configuration 

SSID and bridge between Wireless and Ethernet interfaces is already configured. It's recommended to set up Wireless password and change SSID. If device has been reset, you can also set correct mode and enable interface. 

One liner that does all previously mentioned steps: 

```
/interface w60g set wlan60-1 password="put_your_safe_password_here" ssid="put_your_new_ssid_here" disabled=no
mode=ap-bridge
```

Wireless Wire and wAP60G units come pre-configured with PTP Bridge default configuration. 

Wireless Wire devices have already randomly generated matching SSID and Wireless password. 

Bridge device (Bridge or Access point device with one connected client support) needs Wireless mode change to station-bridge. 

One liner that can be used to set devices in client mode: 

```
/interface w60g set wlan60-1 password="put_your_safe_password_here" ssid="put_your_new_ssid_here" disabled=no
mode=station-bridge
```

If configuration is done from empty configuration (reset without default configuration) - 

new bridge needs to be created containing Wireless and Ethernet interfaces and IP address for easy access should be added. 

1430 

```
{ /interface bridge
```

```
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether1
add bridge=bridge1 interface=wlan60-1
```

```
/ip address add address=192.168.88.1/24 interface=bridge1
```

```
}
```

For Access Point add this line to ensure all connected stations will be put in same bridge. 

```
/interface w60g set wlan60-1 put-stations-in-bridge=bridge1
```

After successful connection for each Client device new entry will appear on Access Point device under: 

```
/interface w60g station print
```

```
Flags: X - disabled, R - running
```

```
0 name="wlan60-station-1" parent=wlan60-1 remote-address=AA:AA:AA:AA:AA:AA mtu=1500 mac-address=AA:AA:AA:AA:AA:
AB arp=enabled arp-timeout=auto put-in-bridge=parent
```

- **`0 name="wlan60-station-2" parent=wlan60-1 remote-address=AA:AA:AA:AA:AB:AA mtu=1500 mac-address=AA:AA:AA:AA:AA: AC arp=enabled arp-timeout=auto put-in-bridge=parent`** 

- **`0 name="wlan60-station-3" parent=wlan60-1 remote-address=AA:AA:AA:AA:AC:AA mtu=1500 mac-address=AA:AA:AA:AA:AA: AD arp=enabled arp-timeout=auto put-in-bridge=parent`** 

- **`0 name="wlan60-station-4" parent=wlan60-1 remote-address=AA:AA:AA:AA:AD:AA mtu=1500 mac-address=AA:AA:AA:AA:AA: AE arp=enabled arp-timeout=auto put-in-bridge=parent`** 

For each client separate settings can be applied (queues, VLANS, Firewall rules, etc) providing more flexibility in configuration. 

To limit client-client communication in same bridge isolate-stations option can be used on Access Point device: 

```
/interface w60g set wlan60-1 isolate-stations=yes
```
