## NTP Client properties: 

**==> picture [516 x 430] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (yes, no default:  Enable NTP client for time synchronization<br>no)<br>mode  (broadcast,  Mode that the NTP client will operate in<br>manycast, multicast,<br>unicast)<br>NTP servers The list of NTP servers. It is possible to add static entries.<br>The following formats are accepted:<br>- FQDN ("Resolved Address" will appear in the "Servers"- window in an appropriate column if the address is resolved) or IP<br>address can be used. If DHCP-Client property  use-peer-ntp=yes  - the dynamic entries advertised by DHCP<br>- ipv4<br>- ipv4 @ vrf<br>- ipv6<br>- ipv6 @ vrf<br>- ipv6-linklocal % interface<br>vrf  (default: main) Virtual Routing and Forwarding<br>Servers  (Button/Section) A detailed table of dynamically and statically added NTP servers (Address, Resolved address, Min Poll, Max Poll, iBurst,<br>Auth. Key)<br>To set the NTP server using its FQDN. The domain name will be resolved each time an NTP request is sent. Router has to<br>have /ip/dns configured.<br>Peers Current parameter values<br>[admin@ntp-example_v7] > /system/ntp/monitor-peers<br> type="ucast-client" address=x.x.x.x refid="y.y.y.y" stratum=3 hpoll=10 ppoll=10 root-<br>delay=28.869 ms root-disp=50.994 ms<br>   offset=-0.973 ms delay=0.522 ms disp=15.032 ms jitter=0.521 ms<br>-- [Q quit|D dump|C-z pause]<br>Keys NTP symmetric keys, used for authentication between the NTP client and server. Key Identifier (Key ID) - an integer<br>identifying the cryptographic key used to generate the message-authentication code.<br>**----- End of picture text -----**<br>


1155 

Status 

synchronized, stopped, waiting, using-local-clock - Current status of the NTP client Frequency drift - The fractional frequency drift per unit time. synced-server - The IP address of the NTP Server. synced-stratum - The accuracy of each server is defined by a number called the stratum, with the topmost level (primary servers) assigned as one and each level downwards (secondary servers) in the hierarchy assigned as one greater than the preceding level. system-offset - This is a signed, fixed-point number indicating the offset of the NTP server's clock relative to the local clock, in seconds.
