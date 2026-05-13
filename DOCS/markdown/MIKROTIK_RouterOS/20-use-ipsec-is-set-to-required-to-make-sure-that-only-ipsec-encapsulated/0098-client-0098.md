## Client 

On client side we need to set up PPPoE client interface and run DHCP client on it. 

```
/interface pppoe-client
```

```
add name=client-test interface=ether1 user=a1 service-name=test
```
