## FastTrack 

IPv4 FastTrack is a special handler that bypasses Linux facilities allowing for faster packet forwarding. The handler is used for TCP and UDP connections marked with " `fasttrack-connection` " action. IPv4 FastTrack handler supports NAT (SNAT, DNAT, or both). 

Note that not all packets of the connection can be FastTracked, so it is likely to see some packets going through a slow path even though the connection is marked for FastTrack. This is the reason why fasttrack-connection is usually followed by an identical " _`action=accept`_ " rule. 

FastTrack-ed packets are bypassing: 

firewall, connection tracking, simple queues, queue tree with parent=global, IP accounting, IPSec, hotspot universal client, VRF assignment 

It is up to the administrator to make sure FastTrack does not interfere with other configuration.
