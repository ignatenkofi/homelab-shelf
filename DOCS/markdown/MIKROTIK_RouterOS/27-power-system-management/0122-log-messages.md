## Log messages 

Sub-menu level: **`/log`** 

All messages stored in routers local memory can be printed from `/log` menu. Each entry contains time and date when event occurred, topics that this message belongs to and message itself. 

```
[admin@MikroTik] /log> print
jan/02/1970 02:00:09 system,info router rebooted
sep/15 09:54:33 system,info,account user admin logged in from 10.1.101.212 via winbox
sep/15 12:33:18 system,info item added by admin
sep/15 12:34:26 system,info mangle rule added by admin
sep/15 12:34:29 system,info mangle rule moved by admin
sep/15 12:35:34 system,info mangle rule changed by admin
sep/15 12:42:14 system,info,account user admin logged in from 10.1.101.212 via telnet
sep/15 12:42:55 system,info,account user admin logged out from 10.1.101.212 via telnet
01:01:58 firewall,info input: in:ether1 out:(none), src-mac 00:21:29:6d:82:07, proto UDP,
10.1.101.1:520->10.1.101.255:520, len 452
```

If logs are printed at the same date when log entry was added, then only time will be shown. In example above you can see that second message was added on sep/15 current year (year is not added) and the last message was added today so only the time is displayed. 

Print command accepts several parameters that allows to detect new log entries, print only necessary messages and so on. 

For example following command will print all log messages where one of the topics is info and will detect new log entries until Ctrl+C is pressed. 

```
[admin@MikroTik] /log > print follow where topics~".info"
12:52:24 script,info hello from script
-- Ctrl-C to quit.
```

In this example it will print only the dhcp info messages: 

1771 

```
[admin@MikroTik] log/print where topics~"dhcp.info"
```

```
11:42:32 dhcp,info defconf deassigned 192.168.88.37 for B0:E4:5C:27:EF:F2 Samsung
```

```
11:42:32 dhcp,info defconf assigned 192.168.88.37 for B0:E4:5C:27:EF:F2 Samsung
```

If print is in follow mode you can hit 'space' on keyboard to insert separator: 

```
[admin@MikroTik] /log > print follow where topics~".info"
12:52:24 script,info hello from script
```

```
= = = = = = = = = = = = = = = = = = = = = = = = = = =
```

```
-- Ctrl-C to quit.
```
