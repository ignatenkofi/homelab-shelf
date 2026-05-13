## Verify that IP connectivity and routing are working properly 

```
[admin@R4] /ip/address> /tool traceroute 111.111.111.1 src-address=111.111.111.4
Columns: ADDRESS, LOSS, SENT, LAST, AVG, BEST, WORST, STD-DEV
#  ADDRESS        LOSS  SENT  LAST   AVG  BEST  WORST  STD-DEV
1  111.13.0.1     0%       4  0.6ms  0.6  0.6   0.6    0
2  111.12.0.1     0%       4  0.5ms  0.6  0.5   0.6    0.1
3  111.111.111.1  0%       4  0.6ms  0.6  0.6   0.6    0
```
