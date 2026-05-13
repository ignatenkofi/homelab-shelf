## Query current configuration: 

- `[admin@MikroTik] > interface/lte/at-chat lte1 input="AT+QNWLOCK=\"common/5g\"" output: +QNWLOCK: "common/5g",138,628032,30,78` 

- `OK` 

To remove the cell lock use this at-chat command: 

```
/interface/lte/at-chat lte1 input="AT+QNWLOCK=\"common/5g\",0"
```

**==> picture [13 x 13] intentionally omitted <==**

1. Cell lock information will not be saved after a reboot or modem reset. 

2. AT+QNWLOCK command can lock the cell and frequency. Therefore, the module can be given priority to register to the locked cell, however, according to the 3gpp protocol, the module will be redirected or handover to a cell with better signal instructions, even if it is not within the lock of the command. This phenomenon is normal. 

3. When locking a cell, please make sure that the module supports the frequency band corresponding to the locked cell, otherwise an error code will be returned. 

4. AT+QNWLOCK="common/5g" does not support locking 5G cells of NSA. (You can still lock to the lte anchor cell using the AT+QNWLOCK=" common/4g" command.) 

5. This Write Command can only be executed when the module is in full functionality (lte interface is not disabled). 

6. This command is not recommended for commercial use. 

for FG621-EA 

822 

```
AT+GTCELLLOCK=<mode>[,<rat>,<type>,<earfcn>[,<PCI>]]
```

```
where
```

```
< mode >: integer type; 0 Disable this function 1 Enable this function 2 Add new cell to be locked
```

```
<rat>: integer type; 0 LTE 1 WCDMA
```

```
<type>: integer type; 0 Lock PCI 1 Lock frequency
```

```
<earfcn>: integer type; the range is 0-65535.
```

```
<PCI>: integer type; If second parameter value is 0, the range is 0-503 for LTE If second parameter value is 1,
the rang is 0-512 for WCDMA
```
