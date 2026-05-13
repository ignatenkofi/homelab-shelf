## Site 1 (server) configuration 

This is the side that will listen to incoming connections and act as a responder. We will use mode config to provide an IP address for the second site, but first, create a loopback (blank) bridge and assign an IP address to it that will be used later for GRE tunnel establishment. 

1210 

```
/interface bridge
add name=loopback
/ip address
```

```
add address=192.168.99.1 interface=loopback
```

Continuing with the IPsec configuration, start off by creating a new Phase 1 profile and Phase 2 proposal entries using stronger or weaker encryption parameters that suit your needs. Note that this configuration example will listen to all incoming IKEv2 requests, meaning the profile configuration will be shared between all other configurations (e.g. RoadWarrior).
