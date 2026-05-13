## Configuration example 

In the following example, we will mark all the packets coming from preconfigured in-interface-list=LAN and will limit the traffic with a queue tree based on these packet marks. 

Let`s create a firewall address-list: 

```
[admin@MikroTik] > /ip firewall address-list
add address=www.youtube.com list=Youtube
[admin@MikroTik] > ip firewall address-list print
Flags: X - disabled, D - dynamic
 #   LIST
ADDRESS                                                                        CREATION-TIME
TIMEOUT
 0   Youtube                                                    www.youtube.
com                                                                oct/17/2019 14:47:11
 1 D ;;; www.youtube.com
     Youtube
216.58.211.14                                                                  oct/17/2019 14:47:11
 2 D ;;; www.youtube.com
     Youtube
216.58.207.238                                                                 oct/17/2019 14:47:11
 3 D ;;; www.youtube.com
     Youtube
216.58.207.206                                                                 oct/17/2019 14:47:11
 4 D ;;; www.youtube.com
     Youtube
172.217.21.174                                                                 oct/17/2019 14:47:11
 5 D ;;; www.youtube.com
     Youtube
216.58.211.142                                                                 oct/17/2019 14:47:11
 6 D ;;; www.youtube.com
     Youtube
172.217.22.174                                                                 oct/17/2019 14:47:21
 7 D ;;; www.youtube.com
     Youtube
172.217.21.142                                                                 oct/17/2019 14:52:21
```

Mark packets with firewall mangle facility: 

```
[admin@MikroTik] > /ip firewall mangle
add action=mark-packet chain=forward dst-address-list=Youtube in-interface-list=LAN new-packet-mark=pmark-
Youtube passthrough=yes
```

Configure the queue tree based on previously marked packets: 

```
[admin@MikroTik] /queue tree
add max-limit=5M name=Limiting-Youtube packet-mark=pmark-Youtube parent=global
```

Check Queue tree stats to be sure traffic is matched: 

```
[admin@MikroTik] > queue tree print stats
Flags: X - disabled, I - invalid
```

```
 0   name="Limiting-Youtube" parent=global packet-mark=pmark-Youtube rate=0 packet-rate=0 queued-bytes=0 queued-
packets=0 bytes=67887 packets=355 dropped=0
```

699
