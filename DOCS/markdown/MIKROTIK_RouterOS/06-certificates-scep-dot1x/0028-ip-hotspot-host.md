## IP HotSpot Host 

```
/ip/hotspot/host
```

The host table lists all computers connected to the HotSpot server. The host table is informational and it is not possible to change any value there: 

**==> picture [516 x 91] intentionally omitted <==**

**----- Start of picture text -----**<br>
Parameters Description<br>mac-address  (read-only; MAC- HotSpot user MAC-address<br>address)<br>address  (read-only; IP address) HotSpot client original IP address<br>to-address  (read-only; IP address) The new client address assigned by HotSpot might be the same as the original  address<br>**----- End of picture text -----**<br>


294 

**==> picture [516 x 200] intentionally omitted <==**

**----- Start of picture text -----**<br>
server  (read-only; name) HotSpot server name client is connected to<br>bridge-port  (read-only; name) "/interface bridge port" the client is connected to, value is unknown when HotSpot is not configured on the<br>bridge<br>uptime  (read-only; time) value shows how long the user is online (connected to the HotSpot)<br>idle-time  (read-only; time) time user has been idle<br>idle-timeout  (read-only; time)  value of the client idle-timeout (unauthorized client)<br>keepalive-timeout  (read-only; time) keepalive-timeout value of the unauthorized client<br>bytes-in  (read-only; integer) amount of bytes received from an unauthorized client<br>packet-in  (read-only; integer) amount of packets received from an unauthorized client<br>bytes-out  (read-only; integer) amount of bytes sent to an unauthorized client<br>packet-out  (read-only; integer)  amount of packets sent to an unauthorized client<br>**----- End of picture text -----**<br>
