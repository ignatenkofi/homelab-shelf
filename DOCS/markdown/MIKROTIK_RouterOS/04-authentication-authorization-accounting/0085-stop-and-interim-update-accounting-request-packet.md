## Stop and Interim-Update Accounting-Request packet 

Additionally to the accounting start request, the following messages will contain the following attributes: 

318 

- Acct-Session-Time - connection uptime in seconds Acct-Input-Octets - bytes received from the client Acct-Input-Gigawords - 4G (2^32) bytes received from the client (bits 32..63, when bits 0..31 are delivered in Acct-Input-Octets) Acct-Input-Packets - nubmer of packets received from the client Acct-Output-Octets - bytes sent to the client Acct-Output-Gigawords - 4G (2^32) bytes sent to the client (bits 32..63, when bits 0..31 are delivered in Acct-Output-Octets) Acct-Output-Packets - number of packets sent to the client
