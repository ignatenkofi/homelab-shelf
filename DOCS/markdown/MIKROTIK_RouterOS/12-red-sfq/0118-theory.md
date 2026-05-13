## Theory 

Each entry in the connection tracking table represents bidirectional communication. Every time a packet gets associated with a particular entry, the packet size value (including the IP header) is added to the "connection-bytes" value for this entry. (in other words "connection-bytes" includes both - upload and download). 

Connection Rate calculates the speed of connection based on the change of "connection-bytes". The connection rate is recalculated every second and does not have any averages. 

Both options "connection-bytes" and "connection-rate" work only with TCP and UDP traffic. (you need to specify a protocol to activate these options). In the "connection-rate" you can specify a range of speed that you like to capture: 

```
ConnectionRate ::= [!]From-To
  From,To ::= 0..4294967295    (integer number)
```
