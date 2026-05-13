## Locking band on Huawei and other modems 

To lock band for Huawei modems `/interface lte set lte1 band=""` option can't be used. 

It is possible to use AT commands to lock to the desired band manually. 

To check all supported bands run the at-chat command: 

823 

```
[admin@MikroTik] /interface lte at-chat lte1 input="AT^SYSCFGEX=\?"
```

```
output: ^SYSCFGEX: ("00","03","02","01","99"),((2000004e80380,"GSM850/GSM900/GSM1800/GSM1900/WCDMA BCI/WCDMA
BCII/WCDMA BCV/WCDMA BCVIII"),
```

```
(3fffffff,"All Bands")),(0-2),(0-4),((800d7,"LTE BC1/LTE BC2/LTE
BC3/LTE BC5/LTE BC7/LTE BC8/LTE BC20"),(7fffffffffffffff,"All Bands"))
OK
```
