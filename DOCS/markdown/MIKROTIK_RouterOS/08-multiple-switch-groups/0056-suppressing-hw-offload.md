## Suppressing HW Offload 

By default, all the routes are participating to be hardware candidate routes. To further fine-tune which traffic to offload, there is an option for each route to disable/enable **`suppress-hw-offload`** . 

For example, if we know that the majority of traffic flows to the network where servers are located, we can enable offloading only to that specific destination: 

```
/ip/route set [find where static && dst-address!="192.168.3.0/24"] suppress-hw-offload=yes
```

Now only the route to 192.168.3.0/24 has H-flag, indicating that it will be the only one eligible to be selected for HW offloading: 

```
[admin@MikroTik] > /ip/route print where static
Flags: A - ACTIVE; s - STATIC, y - COPY; H - HW-OFFLOADED
Columns: DST-ADDRESS, GATEWAY, DISTANCE
#     DST-ADDRESS       GATEWAY         D
0 As  0.0.0.0/0         172.16.2.1      1
1 As  10.0.0.0/8        10.155.121.254  1
2 AsH 192.168.3.0/24    172.16.2.1      1
```

**==> picture [13 x 13] intentionally omitted <==**

H-flag does not indicate that the route is actually HW offloaded, it indicates only that the route can be selected to be HW offloaded.
