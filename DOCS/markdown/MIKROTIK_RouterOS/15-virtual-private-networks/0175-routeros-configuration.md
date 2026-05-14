## RouterOS configuration 

Add a new WireGuard interface and assign an IP address to it. 

```
/interface wireguard
add listen-port=13231 name=wireguard1
/ip address
add address=192.168.100.1/24 interface=wireguard1
```

Adding a new WireGuard interface will automatically generate a pair of private and public keys. You will need to configure the public key on your remote devices. To obtain the public key value, simply print out the interface details. 

```
[admin@home] > /interface wireguard print
```

```
Flags: X - disabled; R - running
```

```
 0  R name="wireguard1" mtu=1420 listen-port=13231 private-key="cBPD6JNvbEQr73gJ7NmwepSrSPK3np381AWGvBk/QkU="
      public-key="VmGMh+cwPdb8//NOhuf1i1VIThypkMQrKAO9Y55ghG8="
```

For the next steps, you will need to figure out the public key of the remote device. Once you have it, add a new peer by specifying the public key of the remote device and allowed addresses that will be allowed over the WireGuard tunnel.
