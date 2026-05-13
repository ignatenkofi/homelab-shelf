## Advanced: HAProxy with Certbot 

This example shows how to configure HAProxy to serve HTTPS traffic and automatically renew the certificates by using Certbot and RFC2136. 

1.  Create HAProxy Container: 

1865 

```
/container/mounts/add name=MOUNT_HAPROXY src=disk1/volumes/haproxy/config dst=/usr/local/etc/haproxy
/container/add remote-image=haproxy:latest interface=veth1 root-dir=disk1/images/haproxy
mounts=MOUNT_HAPROXY name=haproxy start-on-boot=yes user=0:0 logging=yes
```

2.  Create a new file called `haproxy.cfg` on your PC and upload it to `disk1/volumes/haproxy/config/` , adjust the configuration to your needs: 

```
global
  log stdout format raw local0 info
  stats socket :9999 level admin expose-fd listeners
  ssl-default-bind-ciphers EECDH+AESGCM:EDH+AESGCM
  ssl-default-server-ciphers EECDH+AESGCM:EDH+AESGCM
  ssl-default-bind-options ssl-min-ver TLSv1.2
  ssl-default-server-options ssl-min-ver TLSv1.2
  tune.ssl.default-dh-param 2048
  tune.bufsize 43768
  tune.ssl.cachesize 1000000
  nbthread 8
defaults
  log global
  timeout client 10s
  timeout connect 10s
  timeout server 10s
  timeout http-request 10s
frontend frontend_webapp
  mode http
  option httplog
  option http-server-close
  option forwardfor except 127.0.0.0/8
  stick-table type ipv6 size 100k expire 30s store http_req_rate(10s)
  http-request track-sc0 src
  http-request deny deny_status 429 if { sc_http_req_rate(0) gt 10000 }
  bind *:80
  bind *:443 ssl crt /usr/local/etc/haproxy/certs/
  http-request redirect scheme https unless { ssl_fc }
  http-request set-header X-Forwarded-Host %[req.hdr(host)]
  http-request set-header X-Forwarded-For %[src]
  use_backend backend_webapp
backend backend_webapp
  mode http
  balance roundrobin
  option http-server-close
  option forwardfor
  server server1 172.17.0.2:8080
```
