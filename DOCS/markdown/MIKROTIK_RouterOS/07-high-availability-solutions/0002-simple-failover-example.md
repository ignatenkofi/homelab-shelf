## Simple Failover Example 

Simplest failover setup would be to use multiple gateways when one gateway is active and another one takes over when the first one fails. 

To make this work, configure larger distance value for the secondary one, and check-gateway for the first one: 

```
/ip route add gateway=192.168.1.1 distance=1 check-gateway=ping
/ip route add gateway=192.168.2.1 distance=2
```

The check-gateway will make sure the gateway is up only when actual traffic can reach the gateway. When the ping fails the first gateway will become inactive and the second one will take over,  and when the first gateway recovers  it will become active and make the second gateway to work again as a backup. 

757
