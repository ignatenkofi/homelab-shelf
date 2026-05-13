## Verify Connectivity 

Once the configuration is complete, you should be able to access the internet from the router. To verify IP connectivity, try pinging a known IP address, such as a Google DNS server. 

```
[admin@MikroTik] > /ping 8.8.8.8
  SEQ HOST                                     SIZE TTL TIME       STATUS
    0 8.8.8.8                                    56  55 14ms399us
    1 8.8.8.8                                    56  55 18ms534us
    2 8.8.8.8                                    56  55 14ms384us
```
