## `/ip firewall nat` 

```
add chain=srcnat action=accept place-before=0 src-address=10.1.101.0/24 dst-address=10.1.202.0/24
```

1209 

**==> picture [13 x 13] intentionally omitted <==**

If you previously tried to establish an IP connection before the NAT bypass rule was added, you have to clear the connection table from the existing connection or restart both routers. 

It is very important that the bypass rule is placed at the top of all other NAT rules. 

Another issue is if you have IP/Fasttrack enabled, the packet bypasses IPsec policies. So we need to add accept rule before FastTrack.
