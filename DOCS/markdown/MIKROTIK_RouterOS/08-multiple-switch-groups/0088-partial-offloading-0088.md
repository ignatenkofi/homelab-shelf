## Partial offloading 

450 

The DX8000/DX4000 have entirely different routing tables. Instead of prefixes, we have to offload route indexes. The entire IPv4 address range (same for IPv6) must be indexed, i.e., 0.0.0.0 - 255.255.255.255. Adding new route entries causes index rebuild, increasing hardware memory by 0-5 entries depending on the complexity of the routing table. That's why no exact numbers are given. For example, some routing tables containing 240K entries can be fully offloaded to CRS317 HW, while others with 160K entries barely fit. And you will never know until you try. 

When indexing the entire IP address range (0.0.0.0 - 255.255.255.255), you can offload as many routes as needed, as long as you also have a default route (0.0.0.0/0) using the same next-hop. 

For example, on a CCR2216 router around 950k routes with a /30 prefix are created, all using the same next-hop along with a default route. As a result, all routes were offloaded, while the lmp-usage remained minimal. 

```
[admin@MikroTik] > interface/ethernet/switch/l3hw-settings/advanced/monitor
        ipv4-routes-total: 942338
           ipv4-routes-hw: 942326
          ipv4-routes-cpu:     11
  ipv4-shortest-hw-prefix:      0
               ipv4-hosts:      1
         route-queue-size:      0
         route-queue-rate:      0
       route-process-rate:      0
              nexthop-cap:   8192
            nexthop-usage:     85
    vxlan-mtu-packet-drop:      0
     fasttrack-ipv4-conns:      0
     fasttrack-queue-size:      0
     fasttrack-queue-rate:      0
   fasttrack-process-rate:      0
   fasttrack-hw-min-speed:      0
   fasttrack-hw-offloaded:      0
    fasttrack-hw-unloaded:      0
                  lpm-cap:  27200
                lpm-usage:     11
             lpm-bank-cap:   1360
           lpm-bank-usage:      1
                                0
                                0
                                0
                                1
                                0
                                0
                                0
                                4
                                0
                                0
                                0
                                5
                                0
                                0
                                0
                                0
                                0
                                0
                                0
                  pbr-cap:   8192
                pbr-usage:      0
             pbr-lpm-bank:      2
                nat-usage:      0
```

However, if there are "gaps" in the address range, such as not using a default route or having multiple next-hops, this consumes HW table. When the routing HW table gets full, only routes with longer subnet prefixes are offloaded (/30, /29, /28, etc.) while the CPU processes the shorter prefixes. Here is what happens when the default route gets disabled or different next-hops are used: only 37k routes with a /30 prefix fit in the HW table. This is the worstcase scenario for the CCR2216. 

451 

```
[admin@MikroTik] > interface/ethernet/switch/l3hw-settings/advanced/monitor
        ipv4-routes-total: 942337
           ipv4-routes-hw:  37729
          ipv4-routes-cpu: 904608
  ipv4-shortest-hw-prefix:     30
               ipv4-hosts:      1
         route-queue-size:      0
         route-queue-rate:      0
       route-process-rate:      0
              nexthop-cap:   8192
            nexthop-usage:     85
    vxlan-mtu-packet-drop:      0
     fasttrack-ipv4-conns:      0
     fasttrack-queue-size:      0
     fasttrack-queue-rate:      0
   fasttrack-process-rate:      0
   fasttrack-hw-min-speed:      0
   fasttrack-hw-offloaded:      0
    fasttrack-hw-unloaded:      0
                  lpm-cap:  27200
                lpm-usage:  22392
             lpm-bank-cap:   1360
           lpm-bank-usage:   1022
                             1033
                             1027
                             1028
                             1221
                             1033
                             1040
                              678
                             1358
                             1245
                             1254
                             1242
                             1246
                             1249
                             1273
                             1260
                             1101
                             1024
                             1031
                             1027
                  pbr-cap:   8192
                pbr-usage:      0
             pbr-lpm-bank:      2
                nat-usage:      0
```

In many cases, the default behavior "offloading only routes with longer subnet prefixes" is not optimal, especially if the ratio of CPU-handled routes to HWoffloaded routes is too high. When this happens, the chances of a packet being hardware-forwarded drop significantly. 

If HW memory is insufficient and partial offloading occurs, a better approach for you as a network administrator would be to offload only the routes that carry the most traffic while keeping less demanding routes on the CPU, and not letting the partial offloading to happen. 

Fortunately, there are several ways to manage this. There is per-switch-port and static route suppression, and filtering dynamic routes using a wide range of attributes. One example is to use as-path to filter most demanding prefixes (Google, Meta), while all other routes gets L3HW suppressed. 

452
