## Syntax 

```
 :cmd SECRET script NAME [[ VAR[=VAL] ] ... ]
```

SECRET - the password 

NAME - the name of the script that's available in " `/system script` " VAR - variables that will be passed to the script (can be passed as VAR or as VAR=value), separated by spaces. 

Other things to remember: 

*Parameters can be put into quotes "VAR"="VAL" if necessary. 

829 

- *Escaping of values is not supported (VAR="\""). 

- *Combined SMS are not supported, every SMS will be treated separately 

- 16Bit unicode messages are not supported 

- SMS are decoded with the standard GSM7 alphabet, so you can't send in other encodings, otherwise it will be decoded incorrectly
