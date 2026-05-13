## Connections 

```
/ip/proxy/connections
```

This menu contains the list of current connections the proxy is serving. 

Read-only properties: 

**==> picture [501 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>client  ()<br>dst-address  (Ip4 | Ip6) IPv4/Ipv6 destination address of the connection<br>protocol  (string) Protocol name<br>**----- End of picture text -----**<br>


937 

**==> picture [501 x 271] intentionally omitted <==**

**----- Start of picture text -----**<br>
rx-bytes  (integer) The number of bytes received by the client<br>server  ()<br>src-address  (Ip4 | Ip6) Ipv4/ipv6 address of the connection originator<br>state  (closing | connecting | converting | hotspot | idle | resolving | rx-header | tx- Connection state:<br>body | tx-eof | tx-header | waiting)<br>closing - the data transfer is finished, and the<br>connection is being finalized<br>connecting - establishing toe connection<br>converting - replacing header and footer fields in<br>response or request packet<br>hotspot - check if hotspot authentication allows<br>continuing (for hotspot proxy)<br>idle - staying idle<br>resolving - resolving the server's DNS name<br>rx-header - receiving HTTP header<br>tx-body - transmitting HTTP body to the client<br>tx-eof - writing chunk-end (when converting to chunked<br>response)<br>tx-header - transmitting HTTP header to the client<br>waiting - waiting for transmission from a peer<br>tx-bytes  (integer) The number of bytes sent by the client<br>**----- End of picture text -----**<br>
