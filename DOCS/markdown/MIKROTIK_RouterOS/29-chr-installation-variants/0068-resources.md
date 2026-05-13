## Resources 

Just running the Home Assistant on L009 (without any load/traffic) takes up ~300 MB of RAM: 

```
/system resource print
                   uptime: 4m27s
                  version: 7.13.3 (stable)
               build-time: Jan/24/2024 13:16:46
         factory-software: 7.10
              free-memory: 143.0MiB
             total-memory: 448.0MiB
                      cpu: ARM
```

With the load, it will increase, but for testing, on this specific board, it should be enough. 

1870
