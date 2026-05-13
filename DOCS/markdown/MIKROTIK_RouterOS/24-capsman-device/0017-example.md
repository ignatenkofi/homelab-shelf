## Example 

**==> picture [488 x 376] intentionally omitted <==**

This example uses static WDS links that are dynamically added as mesh ports when they become active. Two different frequencies are used: one for AP interconnections, and one for client connections to APs, so the AP must have at least two wireless interfaces. Of course, the same frequency for all connections also could be used, but that might not work as well because of potential interference issues. 

Repeat this configuration on all APs: 

```
/interface mesh add disabled=no
```

```
/interface mesh port add interface=wlan1 mesh=mesh1
```

```
/interface mesh port add interface=wlan2 mesh=mesh1
```
