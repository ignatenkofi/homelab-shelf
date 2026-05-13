## Monitoring 

To verify TE tunnel's status **`monitor`** command can be used. 

```
/interface traffic-eng monitor 0
tunnel-id: 12
primary-path-state: on-hold
secondary-path-state: established
secondary-path: static
active-path: static
active-lspid: 3
active-label: 66
explicit-route: "S:192.168.55.10/32,L:192.168.55.13/32,L:192.168.55.17/32"
recorded-route: "192.168.55.13[66],192.168.55.17[59],192.168.55.18[3]"
reserved-bandwidth: 5.0Mbps
```
