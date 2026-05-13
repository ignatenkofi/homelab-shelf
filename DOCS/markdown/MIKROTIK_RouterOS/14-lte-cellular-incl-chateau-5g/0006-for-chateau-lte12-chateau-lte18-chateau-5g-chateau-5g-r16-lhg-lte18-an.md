## for Chateau LTE12, Chateau LTE18, Chateau 5G, Chateau 5G R16, LHG LTE18 and ATL LTE18, ATL 5G R16, Chateau 5G R17 ax 

```
AT+QNWLOCK="common/4g",<num of cells>,[[<freq>,<pci>],...]
AT+QNWLOCK=\"common/4g\",1,6300,384
```

```
where
```

```
<num of cells>
number of cells to cell lock
```

```
<freq>
earfcn from lte info
```

```
<pci>
phy-cellid from lte info
```

Single-cell lock example: 

```
/interface lte at-chat lte1 input="AT+QNWLOCK=\"common/4g\",1,3050,448"
```
