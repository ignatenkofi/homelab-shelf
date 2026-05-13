## `where` 

```
<pci> String type. Cell physical ID. 0 indicates disabling locking module to the specified cell.
<freq> Integer type. Cell frequency (earfcn).
```

```
<scs> Integer type. NR sub carrier space. Unit: kHz. For FR1(Sub-6 GHz) FDD band, please set <scs> to 15; for FR1
TDD band, please set <scs> to 30. Otherwise, an error code may be returned.
15
```

```
30
```

```
<band> Integer type. NR5G frequency band.
```

Cell lock example to TDD n78 band with earfn=628032 and phy-cellid=138: 

```
/interface/lte/at-chat lte1 input="AT+QNWLOCK=\"common/5g\",138,628032,30,78"
```
