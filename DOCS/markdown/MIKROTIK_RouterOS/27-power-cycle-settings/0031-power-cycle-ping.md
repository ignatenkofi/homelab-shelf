## Power-cycle ping 

Monitor connected PD with power-cycle-ping feature: 

**==> picture [13 x 13] intentionally omitted <==**

/interface ethernet poe set ether1 power-cycle-ping-enabled=yes power-cycle-ping-address=192.168.88.10 power-cycle-ping-timeout=30s 

In this example, PD attached to ether1 will be continuously monitored using a power-cycle-ping feature, which will send ICMP ping requests and wait for a reply. If PD with IP address 192.168.88.10 will not respond for more than 30s, the PoE-Out port will be switched off for 5s.
