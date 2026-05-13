## Catch run-time errors 

Starting from v6.2 scripting has the ability to catch run-time errors. 

For example, the [code]:reslove[/code] command if failed will throw an error and break the script. 

```
[admin@MikroTik] > { :put [:resolve www.example.com]; :put "lala";}
failure: dns name does not exist
```

Now we want to catch this error and proceed with our script: 

```
:onerror e {:put [:resolve www.example.com]} do={:put "resolver failed"}
:put "lalala"
output:
resolver failed
lala
```
