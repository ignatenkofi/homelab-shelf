## DNS configuration 

DNS facility is used to provide domain name resolution for the router itself as well as for the clients connected to it. 

**==> picture [516 x 112] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>allow-remote-requests  (yes  no| ; Specifies whether to allow router usage as a DNS cache for remote clients. Otherwise, only the router itself will use<br>Default:  no ) DNS configuration.<br>address-list-extra-time  (time;  Extra time added to TTL when creating address list entry.<br>Default:  0s )<br>cache-max-ttl  (time; Default:  1w ) Maximum time-to-live for cache records. In other words, cache records will expire unconditionally after cache-max-<br>TTL time. Shorter TTLs received from DNS servers are respected.<br>**----- End of picture text -----**<br>

916 

**==> picture [516 x 411] intentionally omitted <==**

**----- Start of picture text -----**<br>
cache-size  (integer[64.. Specifies the size of the DNS cache in KiB.<br>4294967295]; Default:  2048 )<br>max-concurrent-queries  (integer Specifies how many concurrent queries are allowed.<br>; Default:  100 )<br>max-concurrent-tcp-sessions  (in Specifies how many concurrent TCP sessions are allowed.<br>teger; Default:  20 )<br>max-udp-packet-size  (integer  Maximum size of allowed UDP packet.<br>[50..65507]; Default:  4096 )<br>mdns-repeat-ifaces  (list of  Once an interface in this list receives an mDNS packet, it will forward it to all other interfaces in this list. Only<br>interfaces; Default: ) supports IPv4.<br>query-server-timeout  (time;  Specifies how long to wait for a query response from a server.<br>Default:  2s )<br>query-total-timeout  (time;  Specifies how long to wait for query response in total. Note that this setting must be configured taking into account<br>Default:  10s ) "query-server-timeout" and the number of used DNS servers.<br>servers  (list of IPv4/IPv6  List of DNS server IPv4/IPv6 addresses<br>addresses; Default: )<br>cache-used  (integer) Shows the currently used cache size in KiB<br>dynamic-server  (IPv4/IPv6 list) List of dynamically added DNS servers from different services, for example, DHCP.<br>doh-max-concurrent-queries  (int Specifies how many DoH concurrent queries are allowed.<br>eger; Default:  50 )<br>doh-max-server-connections  (int Specifies how many concurrent connections to the DoH server are allowed.<br>eger; Default: ) 5<br>doh-timeout  (time; Default:  5s ) Specifies how long to wait for query response from the DoH server.<br>use-doh-server  (string; Default: ) Specified which DoH server must be used for DNS queries. DoH functionality overrides "servers" usage if specified.<br>The server must be specified with an "https://" prefix. Supports only one DoH server.<br>verify-doh-cert   (yes  no| ;  Specifies whether to validate the DoH server, when one is being used. Will use the "/certificate" list in order to verify<br>Default:  no ) server validity.<br>**----- End of picture text -----**<br>

```
[admin@MikroTik] > ip dns print
                      servers:
              dynamic-servers: 10.155.0.1
               use-doh-server:
              verify-doh-cert: no
   doh-max-server-connections: 5
   doh-max-concurrent-queries: 50
                  doh-timeout: 5s
        allow-remote-requests: yes
          max-udp-packet-size: 4096
         query-server-timeout: 2s
          query-total-timeout: 10s
       max-concurrent-queries: 100
  max-concurrent-tcp-sessions: 20
                   cache-size: 2048KiB
                cache-max-ttl: 1d
                   cache-used: 48KiB
```

Dynamic DNS servers are obtained from different facilities available in RouterOS, for example, DHCP client, VPN client, IPv6 Router Advertisements, etc. 

Servers are processed in a queue order - static servers as an ordered list, dynamic servers as an ordered list. When DNS cache has to send a request to the server, it tries servers one by one until one of them responds. After that this server is used for all types of DNS requests. Same server is used for any types of DNS requests, for example, A and AAAA types. If you use only dynamic servers, then the DNS returned results can change after reboot, because servers can be loaded into IP/DNS settings in a different order due to a different speeds on how they are received from facilities mentioned above. 

917 

If at some point the server which was being used becomes unavailable and can not provide DNS answers, then the DNS cache restarts the DNS server lookup process and goes through the list of specified servers once more.
