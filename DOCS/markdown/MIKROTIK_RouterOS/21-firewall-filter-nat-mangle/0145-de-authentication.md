## De-authentication 

Wireless peers can be manually de-authenticated (forcing re-association) by removing them from the registration table. 

```
/interface/wifi/registration-table remove [find where mac-address=02:01:02:03:04:05]
```
