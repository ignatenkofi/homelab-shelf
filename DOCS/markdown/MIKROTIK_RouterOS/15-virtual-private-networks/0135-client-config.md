## Client Config 

Add manually which networks you want to access over the tunnel. 

```
/interface ovpn-client
```

```
add name=ovpn-client1 connect-to=2.2.2.2 user=client1 password=123 disabled=no
/ip route
add dst-address=10.5.8.20 gateway=ovpn-client1
add dst-address=192.168.55.0/24 gateway=ovpn-client1
/ip firewall nat add chain=srcnat action=masquerade out-interface=ovpn-client1
```

1248
