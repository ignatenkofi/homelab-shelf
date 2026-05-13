## 11.  Start the Containter: 

```
/container/start pihole
```

12.  Create a port forwarding for your Container: 

```
/ip firewall nat
add action=dst-nat chain=dstnat dst-address=192.168.88.1 dst-port=80 protocol=tcp to-addresses=172.
17.0.2 to-ports=80
```

13.  You should be able to access the Pi-hole web panel by navigating to `http://192.168.88.1/admin/` in your web browser. 14.  To start using Pi-hole on your devices, change their DNS configuration to use `192.168.88.1` as your DNS server.
