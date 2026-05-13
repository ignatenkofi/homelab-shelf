## Knock to gain access 

To access the board from WAN, a port-knocking client could be used, but a simple bash one-liner with nmap can do the job. 

```
for x in 888,555,222; do nmap -p $x -Pn xx.xx.xx.xx; done
```
