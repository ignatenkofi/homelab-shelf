## `/interface ethernet switch rule` 

```
add switch=switch1 dst-address=10.0.1.2/32 dst-port=3306 ports=ether1 new-dst-ports=""
```

```
add switch=switch1 dst-address=10.0.1.2/32 dst-port=3306 ports=ether2,ether3 redirect-to-cpu=yes
```
