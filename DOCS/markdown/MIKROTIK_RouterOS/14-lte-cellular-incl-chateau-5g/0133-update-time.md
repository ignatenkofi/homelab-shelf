## Update time 

Correct time on a device is important, it causes issues with the system's logs, breaks HTTPS connectivity to the device, tunnel connectivity, and other issues. To have your system's clock updated, you can use NTP or SNTP, though it requires you to specify an IP address for the NTP Server. In most cases, NTP/SNTP is not required in order to simply have a correct time set on the device, for simplicity you can use the IP Cloud's update time service. Below you can find operation details that are relevant to the IP/Cloud's update time service: 

Approximate time (accuracy of several seconds, depends on UDP packet latency) 

Updates time after a reboot and during every DDNS update (when router's WAN IP address changes or after the force-update command is used) Sends encrypted packets to cloud2.mikrotik.com using UDP/15252 port 

Detects time-zone depending on the router's public IP address and our commercial database 

To enable the time update service: 

```
[admin@MikroTik] > /ip cloud set update-time=yes
```

To enable automatic time zone detection: 

```
[admin@MikroTik] > /system clock set time-zone-autodetect=yes
```

**==> picture [13 x 13] intentionally omitted <==**

If `/ip cloud update-time` is set to `auto` , then the device's clock will be updated with MikroTik's Cloud server time (if no NTP or SNTP clien t is enabled).
