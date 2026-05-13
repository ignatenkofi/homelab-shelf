## Configuration 

To setup a HAProxy Contaienr on your RouterOS device, follow these steps bellow. 

**==> picture [13 x 13] intentionally omitted <==**

Make sure you have created a Container network before proceeding. 

1.  Create HAProxy Container mount points: 

```
/container/mounts/add name=haproxy_etc src=disk1/haproxy-etc dst=/usr/local/etc/haproxy
```

2.  Create a HAProxy Container: 

```
/container/add remote-image=haproxy:latest interface=veth1 root-dir=disk1/haproxy mounts=haproxy_etc
user=0:0 name=haproxy
```

3.  Connect to your RouterOS device using a SFTP client (for example, WinSCP when using Microsoft Windows) and create a new file `disk1 /haproxy-etc/haproxy.cfg` , you can use the following config as an example: 

```
defaults
  mode http
  timeout client 10s
  timeout connect 10s
  timeout server 10s
  timeout http-request 10s
frontend http_synapse
  bind *:80
  use_backend synapse
backend synapse
  server server1 172.17.0.2:8008 maxconn 32
```

4.  Start the HAProxy Container: 

```
/container/start [find where name=haproxy]
```
