## Monitoring Advertisements 

RouterOS v7 by default disables monitoring of the BGP output. This allows to significantly reduce resource usage on setups with large routing tables. 

To be able to see output advertisements several steps should be taken: 

enable "output.keep-sent-attributes" in BGP connection configuration run "dump-saved-advertisements" from BGP session menu 

view saved output from "/routing/stats/pcap" menu 

```
[admin@arm-bgp] /routing/bgp/connection>  set 0 output.keep-sent-attributes=yes
[admin@arm-bgp] /routing/bgp/session> print
```

```
Flags: E - established
```

```
 0 E remote.address=10.155.101.183 .as=444 .id=192.168.44.2 .refused-cap-opt=no .capabilities=mp,rr,gr,as4
     .afi=ip,ipv6 .messages=4 .bytes=219 .eor=""
```

```
     local.address=10.155.101.186 .as=456 .id=10.155.255.186 .capabilities=mp,rr,gr,as4 .afi=ip,ipv6
     .messages=1 .bytes=19 .eor=""
```

```
     output.procid=66 .filter-chain=bgp_out .network=bgp-nets .keep-sent-attributes=yes
     input.procid=66 ebgp
```

```
     hold-time=3m keepalive-time=1m uptime=4s30ms
```

```
[admin@arm-bgp] /routing/bgp/session> dump-saved-advertisements 0 save-to=test_out.pcap
```
