## Logging to file 

To log everything to file, add new log action: 

```
/system logging action add name=file target=disk disk-file-name=log
```

and then make everything log using this new action: 

```
/system logging add action=file
```

You can log only errors there by issuing command: 

```
/system logging add topics=error action=file
```

This will log into files log.0.txt and log.1.txt . 

You can specify maximum size of file in lines by specifying disk-lines-per-file. <file>.0.txt is active file were new logs are going to be appended and once it size will reach maximum it will become <file>.1.txt , and new empty <file>.0.txt will be created. 

You can log into USB flashes or into MicroSD/CF (on Routerboards) by specifying it's directory name before file name. For example, if you have accessible usb flash as usb1 directory under /files, you should issue following command: 

```
/system logging action add name=usb target=disk disk-file-name=usb1/log
```

**==> picture [13 x 13] intentionally omitted <==**

Logging entries from files will be stored back in the memory after reboot. 

1777
