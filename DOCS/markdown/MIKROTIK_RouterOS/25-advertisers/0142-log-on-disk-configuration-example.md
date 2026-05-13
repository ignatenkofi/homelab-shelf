## Log on disk configuration example 

When configuring logging on disk make sure that you create directories in which you want to store the log files manually, as non-existent directories will NOT be automatically created in this case. 

```
[admin@MikroTik] >  /system logging action set disk disk-file-name=/disk1/log
```

```
...
[admin@MikroTik] >  /file print where name~"disk1/log"
 # NAME                                              TYPE                             SIZE CREATION-TIME
 0 disk1/log                                        directory                             jul/03/2015 12:44:09
 1 disk1/log/syslog.0.txt                           .txt file                         160 jul/03/2015 12:44:11
```

**==> picture [13 x 13] intentionally omitted <==**

Note: Logging topics such as firewall, web-proxy and some other topics that tend to save a large amount or rapid printing of logs on system NAND disk might cause it to wear out faster, so using some attached storage or remote logging is recommended in this case or save data in RAM folder
