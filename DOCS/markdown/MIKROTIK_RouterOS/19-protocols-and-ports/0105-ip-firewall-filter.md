## `/ip firewall filter` 

```
add chain=forward action=accept place-before=1
```

```
src-address=10.1.101.0/24 dst-address=10.1.202.0/24 connection-state=established,related
add chain=forward action=accept place-before=1
```

```
src-address=10.1.202.0/24 dst-address=10.1.101.0/24 connection-state=established,related
```

However, this can add a significant load to the router's CPU if there is a fair amount of tunnels and significant traffic on each tunnel. 

The solution is to use IP/Firewall/Raw to bypass connection tracking, that way eliminating the need for filter rules listed above and reducing the load on CPU by approximately 30%.
