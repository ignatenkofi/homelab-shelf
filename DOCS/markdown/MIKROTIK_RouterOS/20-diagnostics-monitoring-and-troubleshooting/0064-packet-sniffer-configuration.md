## Packet Sniffer configuration 

RouterOS embedded sniffer allows you to capture packets based on various protocols. 

In the following example, we will configure the sniffer to match packets going through the ether1 interface: 

```
[admin@MikroTik] > /tool/sniffer/start interface=ether1
[admin@MikroTik] > /tool/sniffer/stop
[admin@MikroTik] > /tool/sniffer/save file-name=/flash/test.pcap
MikroTik] > file print where name~"test"
Columns: NAME, TYPE, SIZE, CREATION-TIME
#  NAME        TYPE  SIZE  CREATION-TIME
9  flash/test.pcap  file  3696  dec/04/2019 10:48:16
```

You can download captured packets from a file section. Then you can use a packet analyzer such as Wireshark to analyze a file: 

**==> picture [505 x 36] intentionally omitted <==**

If you are using packet streaming to PC and are using Wireshark, to ensure you are only viewing the streamed data, you will need to apply a filter that matches the port the sniffer is using, by default 37008 is used. In addition, we recommend using `filter-stream=yes` . 

**==> picture [144 x 113] intentionally omitted <==**

1795 

**==> picture [13 x 13] intentionally omitted <==**

Please note that sniffed packets will be available for 10 minutes, if you need them permanently, set a "file-name" to save them directly or issue a "save" command as described previously. 

**==> picture [13 x 13] intentionally omitted <==**

Starting with RouterOS 7.20, the sniffer tool saves captured packets in PCAPNG format, which is not supported by the traffic-generator injectpcap feature.
