## Basic multicast routing on single device 

Picture this scenario, you have got a router with two interfaces, namely ether1 and ether2, and each of them is set up in separate networks. Normally, the router will create connected routes and hosts on both networks will be able to communicate using unicast traffic. However, if you want to enable multicast communication between these networks, you'll need to configure multicast routing separately because it won't work otherwise. In this scenario, we are going to create a simple configuration. This involves creating a PIM instance and configuring the required interfaces. 

1087 

**==> picture [504 x 253] intentionally omitted <==**

Begin by ensuring that IP addresses are set up on the router's interfaces. 

```
/ip address
add address=192.168.10.1/24 interface=ether1 network=192.168.10.0
add address=192.168.20.1/24 interface=ether2 network=192.168.20.0
```

Configure PIM instance. For this example, the default settings should work fine. 

```
/routing pimsm instance
add name=pimsm-instance-1
```

Last, add interfaces and specify the PIM instance you created earlier. 

```
/routing pimsm interface-template
add interfaces=ether1,ether2 instance=pimsm-instance-1
```

Now router starts listening to IGMP membership reports (client join messages) and will route multicast traffic to clients interested in receiving it. 

To test the configuration, you can configure a multicast sender using RouterOS traffic-generator and IGMP client using GMP. 

```
# Multicast Sender
/ip address
add address=192.168.10.10/24 interface=ether1 network=192.168.10.0
/tool traffic-generator packet-template
```

```
add interface=ether1 ip-dst=229.1.1.2 mac-dst=01:00:5E:01:01:02/FF:FF:FF:FF:FF:FF name=multicast
/tool traffic-generator quick tx-template=multicast mbps=10
```

```
# Multicast Client
/ip address
add address=192.168.20.10/24 interface=ether1 network=192.168.20.0
/routing gmp
add disabled=no groups=229.1.1.2 interfaces=ether1
```

To verify whether multicast traffic is being properly routed, monitor the received packet counters on the client interface or use tools like Torch or a Packet Sniffer. 

It is also possible to monitor active multicast group on router: 

1088 

```
/routing pimsm uib-g print
Columns: INSTANCE, GROUP
# INSTANCE          GROUP
0 pimsm-instance-1  229.1.1.2
/routing pimsm uib-sg print
Flags: K - KEEPALIVE; S - SPT-BIT
Columns: INSTANCE, GROUP, SOURCE
#    INSTANCE          GROUP      SOURCE
0 KS pimsm-instance-1  229.1.1.2  192.168.10.10
```
