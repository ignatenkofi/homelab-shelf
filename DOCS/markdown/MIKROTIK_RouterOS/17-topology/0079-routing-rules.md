## Routing Rules 

Routing rules allow steering traffic based on basic parameters like a source address, a destination address, or in-interface as well as other parameters. 

For our example, we want to select traffic with destination 8.8.8.8 and do not fall back to the main table: 

```
/routing rule add dst-address=8.8.8.8 action=lookup-only-in-table table=myTable
```

Lets's say that we know that customer is connected to ether4 and we want only that customer to route 8.8.8.8 to a specific gateway. We can use the following rule: 

```
/routing rule add dst-address=8.8.8.8 action=lookup-only-in-table table=myTable interface=ether4
```

If for some reason the gateway used in our table goes down, the whole lookup will fail and the destination will not be reachable. In active-backup setups we want the traffic to be able to fall back to the main table. To do that change the action from `lookup-only-in-table` to `lookup` . 

Also, routing rules can be used as a very "basic firewall". Let's say we do not want to allow a customer connected to ether4 to be able to access the 192.168.1.0/24 network: 

```
/routing rule add dst-address=192.168.1.0/24 interface=ether4 action=drop
```

1066
