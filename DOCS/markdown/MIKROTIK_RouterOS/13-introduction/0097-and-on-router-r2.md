## and on router R2: 

```
/interface vrrp print detail
```

```
 0    B name="vrrp1" mtu=1500 mac-address=00:00:5E:00:01:31 arp=enabled interface=ether1 vrid=49
        priority=100 interval=1 preemption-mode=yes authentication=none password=""
        on-backup="" on-master=" version=3 v3-protocol=ipv4
```

As you can see VRRP interface MAC addresses are identical on both routers. Now to check if VRRP is working correctly, try to ping the virtual address from a client and check ARP entries: 

```
[admin@client] > /ping 192.168.1.1
192.168.1.254 64 byte ping: ttl=64 time=10 ms
192.168.1.254 64 byte ping: ttl=64 time=8 ms
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 8/9.0/10 ms
[admin@client] /ip arp> print
Flags: X - disabled, I - invalid, H - DHCP, D - dynamic
 #   ADDRESS         MAC-ADDRESS       INTERFACE
 ...
 1 D 192.168.1.1   00:00:5E:00:01:31 bridge1
```

Now unplug the ether1 cable on router R1. R2 will become VRRP master, and the ARP table on a client will not change but traffic will start to flow over the R2 router. 

**==> picture [13 x 13] intentionally omitted <==**

In case VRRP is used with Reverse Path Filtering, then it is recommended that `rp-filter` is set to `loose` , otherwise, the VRRP interface might not be reachable.
