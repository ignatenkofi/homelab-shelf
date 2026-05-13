## Destination NAT 

**==> picture [505 x 196] intentionally omitted <==**

Network address translation works by modifying network address information in the packet's IP header. Let`s take a look at the common setup where a network administrator wants to access an office server from the internet. 

We want to allow connections from the internet to the office server whose local IP is 10.0.0.3. In this case, we have to configure a destination address translation rule on the office gateway router: 

```
/ip firewall nat add chain=dstnat action=dst-nat dst-address=172.16.16.1 dst-port=22 to-addresses=10.0.0.3
protocol=tcp
```

The rule above translates: when an incoming connection requests TCP port 22 with destination address 172.16.16.1, use the dst-nat action and depart packets to the device with local IP address 10.0.0.3 and port 22. 

**==> picture [13 x 13] intentionally omitted <==**

To allow access only from the PC at home, we can improve our dst-nat rule with "src-address=192.168.88.1" which is a Home`s PC public (this example) IP address. It is also considered to be more secure!
