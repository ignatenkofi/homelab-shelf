## Offloading Fasttrack Connections 

Firewall filter rules have **`hw-offload`** option for Fasttrack, allowing fine-tuning connection offloading. Since the hardware memory for Fasttrack connections is very limited, we can choose what type of connections to offload and, therefore, benefit from near-the-wire-speed traffic. The next example offloads only TCP connections while UDP packets are routed via the CPU and do not occupy HW memory: 

```
/ip/firewall/filter
```

```
add action=fasttrack-connection chain=forward connection-state=established,related hw-offload=yes protocol=tcp
add action=fasttrack-connection chain=forward connection-state=established,related hw-offload=no
add action=accept chain=forward connection-state=established,related
```

442
