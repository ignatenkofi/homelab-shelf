## Host B: 

```
/ip address add address=10.155.101.221 interface=ether1
```

Host C: 

```
/ip address add address=10.155.101.217 interface=ether1
```

Now, let's run a packet sniffer that saves packet dump to the file and run the ping command on Host A: 

```
/tool sniffer
  set file-name=arp.pcap filter-interface=ether1
  start
/ping 10.155.101.217 count=1
  stop
```

Now you can download arp.pcap file from the router and open it in Wireshark for analyzing: 

**==> picture [504 x 46] intentionally omitted <==**

154 

Host A sends ARP message asking who has "10.155.101.217" 

Host C responds that 10.155.101.217 can be reached at 08:00:27:3C:79:3A MAC address Both Host A and Host C now have updated their ARP tables and now ICMP (ping) packets can be sent 

If we look at ARP tables of both host we can see relevant entries, in RouterOS ARP table can be viewed by running command: `/ip arp print` 

```
[admin@host_a] /ip arp> print
Flags: X - disabled, I - invalid, H - DHCP, D - dynamic, P - published,
C - complete
 #    ADDRESS         MAC-ADDRESS       INTERFACE
 0 DC 10.155.101.217  08:00:27:3C:79:3A ether1
 [admin@host_b] /ip arp> print
Flags: X - disabled, I - invalid, H - DHCP, D - dynamic, P - published,
C - complete
 #    ADDRESS         MAC-ADDRESS       INTERFACE
 0 DC 10.155.101.225  08:00:27:85:69:B5 ether1
```
