## RouterOS 

1.  (optional) Create an Interface list (for example, "NetFlow_interfaces") and add interface that need NetFlow data analysis 

```
/interface list
add name=NetFlow_interfaces
/interface list member
add interface=VLAN3000 list=NetFlow_interfaces
```

2.  Configure Traffic-flow to send NetFlow data to your Elastic Agent (10.0.0.2) 

1827 

```
/ip traffic-flow
enabled=yes interfaces=NetFlow_interfaces
/ip traffic-flow target
add dst-address=10.0.0.2
```

3.  You should now start to see NetFlow data being ingested! 4.  Continue the guide to start using Kibana
