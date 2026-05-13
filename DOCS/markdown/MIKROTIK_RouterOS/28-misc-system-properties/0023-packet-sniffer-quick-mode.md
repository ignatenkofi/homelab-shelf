## Packet Sniffer Quick Mode 

The quick mode will display results as they are filtered out with a limited-size buffer for packets. There are several attributes that can be set up for filtering. If no attributes are set current configuration will be used. 

```
[admin@MikroTik] > /tool/sniffer/quick ip-protocol=icmp
Columns: INTERFace, TIME, NUm, DIr, SRC-MAC, DST-MAC, SRC-ADDRESS, DST-ADDRESS, PROTOCOl, SIze, Cpu, FP
INTERF  TIME    NU  DI  SRC-MAC            DST-MAC            SRC-ADDRESS     DST-ADDRESS     PROTOCO  SI  C  FP
ether7  35.472  79  <-  6C:3B:6B:ED:83:69  6C:3B:6B:ED:81:83  10.155.126.252  10.155.126.253  ip:icmp  70  7  no
ether7  35.472  80  ->  6C:3B:6B:ED:81:83  6C:3B:6B:ED:83:69  10.155.126.253  10.155.126.252  ip:icmp  70  7  no
ether1  35.595  81  <-  6C:3B:6B:ED:83:63  6C:3B:6B:ED:81:7D  172.24.24.2     172.24.24.1     ip:icmp  70  4  no
ether1  35.595  82  ->  6C:3B:6B:ED:81:7D  6C:3B:6B:ED:83:63  172.24.24.1     172.24.24.2     ip:icmp  70  4  no
ether7  36.457  83  <-  6C:3B:6B:ED:83:69  6C:3B:6B:ED:81:83  10.155.126.252  10.155.126.253  ip:icmp  70  7  no
ether7  36.457  84  ->  6C:3B:6B:ED:81:83  6C:3B:6B:ED:83:69  10.155.126.253  10.155.126.252  ip:icmp  70  7  no
ether1  36.6    85  <-  6C:3B:6B:ED:83:63  6C:3B:6B:ED:81:7D  172.24.24.2     172.24.24.1     ip:icmp  70  4  no
ether1  36.6    86  ->  6C:3B:6B:ED:81:7D  6C:3B:6B:ED:83:63  172.24.24.1     172.24.24.2     ip:icmp  70  4  no
```

**==> picture [13 x 13] intentionally omitted <==**

Traffic-Generator packets will not be visible using the packet sniffer on the same interface unless the fast-path parameter is set.
