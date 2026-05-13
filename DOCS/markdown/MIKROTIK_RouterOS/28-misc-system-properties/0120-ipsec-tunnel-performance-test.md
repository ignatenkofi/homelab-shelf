## IPsec tunnel performance test 

Consider following test setup 

1838 

**==> picture [504 x 303] intentionally omitted <==**

System Under Test (SUT) consists of two routers connected to a traffic generator server. The connection between both SUT routers is IPSec encrypted. 

The traffic generator will run two streams: 

in a direction from 1.1.1.0/24 network to 2.2.2.0/24 network in a direction from 2.2.2.0/24 network to 1.1.1.0/24 network. 

R1 routing and IPsec setup 

```
/ip address
add address=192.168.33.1/30 interface=ether1
add address=1.1.1.2/24 interface=ether2
/ip route
add dst-address=2.2.2.0/24 gateway=192.168.33.2
/ip ipsec proposal
set default enc-algorithms=aes-128
/ip ipsec peer
add address=192.168.33.2 secret=123
/ip ipsec policy
add sa-src-address=192.168.33.1 sa-dst-address=192.168.33.2 \
    src-address=1.1.1.0/24 dst-address=2.2.2.0/24 tunnel=yes
```

R2 routing and IPsec setup 

1839 

```
/ip address
add address=192.168.33.2/30 interface=ether1
add address=2.2.2.2/24 interface=ether2
```

```
/ip route
add dst-address=1.1.1.0/24 gateway=192.168.33.1
/ip ipsec proposal
set default enc-algorithms=aes-128
```

```
/ip ipsec peer
add address=192.168.33.1 secret=123
```

```
/ip ipsec policy
add sa-src-address=192.168.33.2 sa-dst-address=192.168.33.1 \
    src-address=2.2.2.0/24 dst-address=1.1.1.0/24 tunnel=yes
```
