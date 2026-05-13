## Neighbor Discovery 

MikroTik Neighbor discovery protocol is used to show and recognize other MikroTik routers in the network. Disable neighbor discovery on public interfaces: 

```
/ip neighbor discovery-settings set discover-interface-list=LAN
```
