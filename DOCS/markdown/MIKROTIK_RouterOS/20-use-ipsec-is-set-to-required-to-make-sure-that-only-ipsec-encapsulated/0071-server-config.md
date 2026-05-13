## Server Config 

The first step is to create an IP pool from which client addresses will be assigned and some users. 

```
/ip pool add name=ovpn-pool range=192.168.77.2-192.168.77.254
```

```
/ppp profile add name=ovpn local-address=192.168.77.1 remote-address=ovpn-pool
/ppp secret
add name=client1 password=123 profile=ovpn
add name=client2 password=234 profile=ovpn
```

Assume that the server certificate is already created and named "server" 

```
/interface ovpn-server server add disabled=no certificate=server name=myServer
```
