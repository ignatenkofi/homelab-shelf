## Properties 

**==> picture [501 x 394] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enabled  (yes |  Allows to disable or enable connection tracking. With disabled connection tracking  firewall features listed above will stop<br>no | auto;  working. If set to "auto" connection tracking is disabled until at least one firewall rule is added.<br>Default: auto )<br>liberal-tcp- Enables or disables liberal TCP connection tracking by toggling the kernel parameter  nf_conntrack_tcp_be_liberal .<br>tracking  (yes |  When set to  yes , the system mark only out of window RST segments as INVALID.<br>no; Default: no )<br>Enabling this setting may allow malformed packets that would otherwise be considered  invalid  by the firewall's  con<br>nection-state  matcher. This can increase exposure to certain evasion techniques. This property should be<br>enabled only when troubleshooting or working around known issues.<br>loose-tcp-<br>tracking  (yes;  In case loose-tcp-tracking=yes, the 2nd part (SYN,ACK) and 3rd part (ACK) of the handshake without having seen the first<br>Default: yes ) initial SYN will be considered ESTABLISHED<br>In case loose-tcp-tracking=no, the 2nd part (SYN,ACK) and 3rd part (ACK) without having seen the first initial SYN will be<br>considered INVALID<br>tcp-syn-sent- TCP SYN timeout.<br>timeout  (time;<br>Default: 5s )<br>tcp-syn- TCP SYN timeout.<br>received-timeout<br>(time; Default: 5s<br>)<br>tcp-established- Time after which established TCP connection times out.<br>timeout  (time;<br>Default: 1d )<br>tcp-fin-wait-<br>timeout  (time;<br>Default: 10s )<br>**----- End of picture text -----**<br>


632 

**==> picture [501 x 300] intentionally omitted <==**

**----- Start of picture text -----**<br>
tcp-close-wait-<br>timeout  (time;<br>Default: 10s )<br>tcp-last-ack-<br>timeout  (time;<br>Default: 10s )<br>tcp-time-wait-<br>timeout  (time;<br>Default: 10s )<br>tcp-close-<br>timeout  (time;<br>Default: 10s )<br>udp-timeout  (time Specifies the timeout for UDP connections that have seen packets in one direction<br>; Default: 30s )<br>udp-stream- Specifies the timeout of UDP connections that have seen packets in both directions<br>timeout  (time;<br>Default: 3m )<br>icmp-timeout  (ti ICMP connection timeout<br>me; Default: 10s )<br>generic-timeout  ( Timeout for all other connection entries<br>time; Default: 10m<br>)<br>**----- End of picture text -----**<br>


Read-only properties 

**==> picture [501 x 102] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>max-entries  ( Max amount of entries that the connection tracking table can hold. This value depends on the installed amount of RAM.<br>integer)<br>Note that the system does not create a maximum-size connection tracking table when it starts, it may increase if the situation<br>demands it and the system still has free RAM, but the size will not exceed 1048576<br>total-entries  ( Amount of connections that the connection table currently holds<br>integer)<br>**----- End of picture text -----**<br>
