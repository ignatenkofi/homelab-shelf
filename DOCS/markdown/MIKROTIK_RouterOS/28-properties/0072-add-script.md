## Add script: 

```
/system script
```

```
add name=script1 owner=admin policy=ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon source="
/sy reboot "
```

```
add name=script2 owner=admin policy=ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon source="[:
put output]"
```
