## Transparent proxy configuration example 

RouterOS can also act as a Transparent Caching server, with no configuration required in the customer’s web browser. A transparent proxy does not modify the requested URL or response. RouterOS will take all HTTP requests and redirect them to the local proxy service. This process will be entirely transparent to the user (users may not know anything about a proxy server that is located between them and the original server), and the only difference to them will be the increased browsing speed. 

To enable the transparent mode, the firewall rule in destination NAT has to be added, specifying which connections (to which ports) should be transparently redirected to the proxy. Check proxy settings above and redirect us users (192.168.1.0/24) to a proxy server: 

```
[admin@MikroTik] ip firewall nat> add chain=dstnat protocol=tcp src-address=192.168.1.0/24 dst-port=80
action=redirect to-ports=8080
[admin@MikroTik] ip firewall nat> print
Flags: X - disabled, I - invalid, D - dynamic
 0   chain=dstnat protocol=tcp dst-port=80 action=redirect to-ports=8080
```

The web proxy can be used as a transparent and normal web proxy at the same time. In transparent mode, it is possible to use it as a standard web proxy, too. However, in this case, proxy users may have trouble reaching web pages that are accessed transparently.
