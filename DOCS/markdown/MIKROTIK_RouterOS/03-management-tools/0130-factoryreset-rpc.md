## FactoryReset RPC 

This is CWMP standard RPC, which performs RouterOS configuration factory-reset. The reset process is performed in the same way as executing the command: 

```
/system reset-configuration skip-backup=yes
```

249 

Note that the default factory configuration can be different for each device (see [1]) and execution of this command removes all configurations and executes internally stored default-configuration script. 

Best Practices Guide for preparing CPE with custom factory settings for TR069 https://wiki.mikrotik.com/Tr069-best-practices
