## `/routing/bgp/connection` 

```
add remote.address=10.155.101.0/24 listen=yes template=default local.role=ibgp
```

Now you can monitor the status of all connected and disconnected peers from `/routing bgp session` menu. 

Other great debugging information on all routing processes can be monitored from `/routing stats` menu 

```
[admin@v7_ccr_bgp] /routing/stats/process> print interval=1
```

```
Columns: TASKS, PRIVATE-MEM-BLOCKS, SHARED-MEM-BLOCKS, PSS, RSS, VMS, RETIRED, ID, PID, RPID, PROCESS-TIME,
KERNEL-TIME, CUR-B>
```

- `# TASKS PRIVATE-M SHARED-ME PSS RSS VMS RET ID PID R PROCESS-TI KERN>` 

- `0 routing tables 12.2MiB 20.0MiB 18.7MiB 42.2MiB 83.4MiB 8 main 319 0 19s750ms 8s50> rib >` 

```
connected networks >
```

```
1 fib 512.0KiB 0 7.4MiB 30.9MiB 83.4MiB fib 384 1 5s160ms 22s5>
```

```
2 ospf 1024.0KiB 1024.0KiB 5.9MiB 25.9MiB 83.4MiB 382 ospf 388 1 1m42s170ms 1m31>
connected networks >
```

```
3 fantasy 512.0KiB 0 2061.0KiB 5.9MiB 83.4MiB fantasy 389 1 1s410ms 870m>
```

```
4 configuration and reporting 40.0MiB 512.0KiB 45.0MiB 64.8MiB 83.4MiB static 390 1 12s550ms 1s17>
5 rip 768.0KiB 0 5.3MiB 24.7MiB 83.4MiB rip 387 1 1s380ms 1s20>
connected networks >
```

```
6 routing policy configuration 512.0KiB 256.0KiB 2189.0KiB 6.0MiB 83.4MiB policy 385 1 1s540ms 1s20>
7 BGP service 768.0KiB 0 2445.0KiB 6.2MiB 83.4MiB bgp 386 1 6s170ms 9s38>
8 BGP Input 10.155.101.217 8.8MiB 6.0MiB 15.6MiB 38.5MiB 83.4MiB 20 21338 1 25s170ms 3s23>
BGP Output 10.155.101.217 >
```

- `9 Global memory 256.0KiB global 0 0 >` 

- `-- [Q quit|D dump|C-z pause|right]` 

Route filtering differs a bit from ROSv6. In the BGP template, you can now specify output.filter-chain, output.filter-select, input.filter as well as several input. 

accept-* options. 

Now input.accept-* allows filtering incoming messages directly before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered", 

A very basic example of a BGP input filter to accept prefixes from 192.168.0.0/16 subnet without modifying any attributes. For other prefixes subtract 1 from the received local pref value and set IGP metric to value from OSPF ext. Additionally, we will accept only specific  prefixes from the address list to reduce memory usage 

```
/ip/firewall/address-list
```

```
add list=bgp_list dst-address=192.168.1.0/24
add list=bgp_list dst-address=192.168.0.0/24
add list=bgp_list dst-address=172.16.0.0/24
```

1077 

```
/routing/bgp/template
```

```
set default input.filter=bgp_in .accept-nlri=bgp_list
```
