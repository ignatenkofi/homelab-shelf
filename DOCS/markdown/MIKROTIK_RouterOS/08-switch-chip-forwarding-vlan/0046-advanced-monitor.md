## Advanced Monitor 

An enhanced version of Monitor with extra telemetry data for advanced users. Advanced Monitor contains all data from the basic monitor plus the fields listed below. 

```
/interface/ethernet/switch/l3hw-settings/advanced> monitor once
        ipv4-routes-total: 29968
           ipv4-routes-hw: 29957
          ipv4-routes-cpu: 11
  ipv4-shortest-hw-prefix: 0
               ipv4-hosts: 3
        ipv6-routes-total: 4
           ipv6-routes-hw: 0
          ipv6-routes-cpu: 4
  ipv6-shortest-hw-prefix: 0
               ipv6-hosts: 0
         route-queue-size: 0
         route-queue-rate: 0
       route-process-rate: 0
     fasttrack-ipv4-conns: 0
     fasttrack-queue-size: 0
     fasttrack-queue-rate: 0
   fasttrack-process-rate: 0
   fasttrack-hw-min-speed: 0
   fasttrack-hw-offloaded: 0
    fasttrack-hw-unloaded: 0
                  lpm-cap: 54560
                lpm-usage: 31931
             lpm-bank-cap: 2728
           lpm-bank-usage: 46,0,0,0,2589,2591,1983,0,2728,2728,2728,2728,2728,2728,2728,2728,2728,170,0,0
                  pbr-cap: 8192
                pbr-usage: 0
             pbr-lpm-bank: 3
                nat-usage: 0
              nexthop-cap: 8192
            nexthop-usage: 85
```

Stats 

Property Description 

routeThe rate at which routes are added to the queue for the switch driver processing. In other words, the growth rate of route-queue-size (rout queue-rate es per second) 

438 

**==> picture [516 x 413] intentionally omitted <==**

**----- Start of picture text -----**<br>
route- The rate at which previously queued routes are processed by the switch driver. In other words, the shrink rate of route-queue-size (routes<br>process- per second)<br>rate<br>fasttrack- The number of FastTrack connections in the queue for processing by the switch chip driver.<br>queue-size<br>fasttrack- The rate at which FastTrack connections are added to the queue for the switch driver processing. In other words, the growth rate of  fasttra<br>queue-rate ck-queue-size (connections per second)<br>fasttrack- The rate at which previously queued FastTrack connections are processed by the switch driver. In other words, the shrink rate of  fasttrack<br>process- -queue-size (connections per second)<br>rate<br>fasttrack- The number of FastTrack connections offloaded to the hardware. The counter resets every second (or every monitor interval).<br>hw-<br>offloaded<br>fasttrack- The number of FastTrack connections unloaded from the hardware (redirected to software routing). The counter resets every second (or<br>hw- every monitor interval).<br>unloaded<br>lpm-cap The size of the LPM hardware table (LPM = Longest Prefix Match). LPM stores route indexes for hardware routing. Not every switch chip<br>model uses LPM. Others use TCAM.<br>lpm-usage The number of used LPM blocks. lpm-usage / lpm-cap = usage percentage.<br>lpm-bank- LPM memory is organized in banks - special memory units. The bank size depends on the switch chip model. This value shows the size<br>cap of a single bank (in LPM blocks). lpm-cap / lpm-bank-cap = the number of banks (usually, 20).<br>lpm-bank- Per-bank LPM usage (in LPM blocks)<br>usage<br>pbr-cap The size of the Policy-Based Routing (PBR) hardware table. PBR is used for NAT offloading of FastTrack connections.<br>pbr-usage The number of used PBR entries. pbr-usage / pbr-cap = usage percentage.<br>pbr-lpm- PBR shares LPM memory banks with routing tables. This value shows the LPM bank index shared with PBR (0 = the first bank).<br>bank<br>nat-usage The number of used NAT hardware entries (for FastTrack connections).<br>**----- End of picture text -----**<br>
