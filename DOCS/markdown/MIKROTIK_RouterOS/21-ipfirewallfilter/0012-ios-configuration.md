## iOS configuration 

Download the WireGuard application from the App Store. Open it up and create a new configuration from scratch. 

1274 

**==> picture [322 x 696] intentionally omitted <==**

1275 

First of all give your connection a "Name" and choose to generate a keypair. The generated public key is necessary for peer's configuration on RouterOS side. 

1276 

**==> picture [322 x 696] intentionally omitted <==**

1277 

Specify an IP address in "Addresses" field that is in the same subnet as configured on the server side. This address will be used for communication. For this example, we used 192.168.100.1/24 on the RouterOS side, you can use 192.168.100.2 here. 

If necessary, configure the DNS servers. If allow-remote-requests is set to yes under IP/DNS section on the RouterOS side, you can specify the remote WireGuard IP address here. 

1278 

**==> picture [322 x 696] intentionally omitted <==**

1279 

Click "Add peer" which reveals more parameters. 

The "Public key" value is the public key value that is generated on the WireGuard interface on RouterOS side. 

"Endpoint" is the IP or DNS with port number of the RouterOS device that the iOS device can communicate with over the Internet. 

"Allowed IPs" are set to 0.0.0.0/0 to allow all traffic to be sent over the WireGuard tunnel. 

1280 

**==> picture [322 x 696] intentionally omitted <==**

1281 

```
Depending on your configuration, you may need to add a NAT rule
chain=dstnat action=dst-nat to-ports=port protocol=udp in-interface=interface dst-port=port
```
