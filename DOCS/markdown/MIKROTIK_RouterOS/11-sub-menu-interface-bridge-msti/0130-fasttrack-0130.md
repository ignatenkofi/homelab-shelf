## FastTrack 

Fasttrack can be decoded as Fast Path + Connection Tracking. It allows marking connections as "fast-tracked", marking packets that belong to fasttracked connection will be sent fast-path way. The connection table entry for such a connection now will have a fast-tracked flag. 

**==> picture [494 x 327] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

692 

FastTrack packets bypass firewall, connection tracking, simple queues, queue tree with parent=global, ip traffic-flow, IP accounting, IPSec, hotspot universal client, VRF assignment, so it is up to the administrator to make sure FastTrack does not interfere with other configuration! 

To mark a connection as fast-tracked new action was implemented "fasttrack-connection" for firewall filter and mangle. Currently, only IPv4 TCP and UDP connections can be fast-tracked and to maintain connection tracking entries some random packets will still be sent to a slow path. This must be taken into consideration when designing firewalls with enabled "fasttrack". 

FastTrack handler also supports source and destination NAT, so special exceptions for NATed connections are not required. 

**==> picture [13 x 13] intentionally omitted <==**

Traffic that belongs to a fast-tracked connection travels in FastPath, which means that it will not be visible by other router L3 facilities (firewall, queues, IPsec, IP accounting, VRF assignment, etc). Fasttrack lookups route before routing marks have been set, so it works only with the main routing table. 

The easiest way to start using this feature on home routers is to enable "fasttrack" for all established, related connections:
