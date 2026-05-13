## IPv4 Addressing 

IPv4 uses 4-byte addresses which are segmented in four 8-bit fields called octets. Each octet is converted to a decimal format and separated by a dot. For example: 

```
11000000 10101000 00000011 00011000 => 192.168.3.24
```

The IPv4 network consists of three addresses: 

- network address - a standard way to refer to an IPv4 address assigned to a network. For example, we could refer to the network 192.168.1.0 or 172.16.0.0 as a “Network Address.” 

- broadcast address - a special address for each network that allows communication to all the hosts in that network. The broadcast address uses the highest address in the network range. for example, broadcast address if 192.168.1.0/24 network will be 192.168.1.255 

- host address - any other address that is not a network address and broadcast address can be used as a host address. For example, 192.168.1.2 - 254 host addresses can be used from 192.168.1.0/24 address range 

There are several types of IP addressing 

161 

- unicast - normally refers to a single sender or a single receiver, and can be used for both sending and receiving. Usually, a unicast address is associated with a single device or host, but it is not a one-to-one correspondence. 

- broadcast - address to send data to all possible destinations ("all-hosts broadcast"), which permits the sender to send the data only once, and all receivers receive a copy of it. In the IPv4 protocol, the address 255.255.255.255 is used for local broadcast. In addition, a directed (limited) broadcast can be made by combining the network prefix with a host suffix composed entirely of binary 1s. For example, the destination address used for directed broadcast to devices on the 192.0.2.0/24 network is 192.0.2.255 

- multicast - address associated with a group of interested receivers. In IPv4, addresses 224.0.0.0 through 239.255.255.255 are designated as multicast addresses. The sender sends a single datagram from its unicast address to the multicast group address and the intermediary routers take care of making copies and sending them to all receivers that have joined the corresponding multicast group.
