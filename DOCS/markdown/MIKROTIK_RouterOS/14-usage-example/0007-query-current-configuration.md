## Query current configuration: 

```
/interface lte at-chat lte1 input="AT+QNWLOCK=\"common/4g\""
```

Multiple cells can also be added to the cell lock. For example to lock to two different cells: 

```
/interface lte at-chat lte1 input="AT+QNWLOCK=\"common/4g\",2,3050,448,1574,474"
```

821 

To remove the cell lock use this at-chat command: 

```
/interface lte at-chat lte1 input="at+qnwlock=\"common/4g\",0"
```

**==> picture [13 x 13] intentionally omitted <==**

1. Cell lock information will not be saved after a reboot or modem reset. 2. AT+QNWLOCK command can lock the cell and frequency. Therefore, the module can be given priority to register to the locked cell, however, according to the 3gpp protocol, the module will be redirected or handover to a cell with better signal instructions, even if it is not within the lock of the command. This phenomenon is normal.
