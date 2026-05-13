## Configuration examples 

```
/ip/proxy
```

In MikroTik RouterOS, a proxy configuration is performed in the /ip/proxy menu. See below how to enable the proxy on port 8080 and set up 

192.168.88.254 as the proxy source address: 

930 

```
[admin@MikroTik] > ip/proxy/set enabled=yes port=8080 src-address=192.168.88.254
[admin@MikroTik] > ip/proxy/print
                 enabled: yes
             src-address: 192.168.88.254
                    port: 8080
               anonymous: no
            parent-proxy: ::
       parent-proxy-port: 0
     cache-administrator: webmaster
          max-cache-size: unlimited
   max-cache-object-size: 2048KiB
           cache-on-disk: no
  max-client-connections: 600
  max-server-connections: 600
          max-fresh-time: 3d
   serialize-connections: no
       always-from-cache: no
          cache-hit-dscp: 4
              cache-path: web-proxy
```

**==> picture [13 x 13] intentionally omitted <==**

When setting up a regular proxy service, make sure it serves only your clients and prevents unauthorized access to it by creating a firewall that allows only your clients to use a proxy, otherwise, it may be used as an open proxy.
