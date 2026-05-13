## Variable names are case-sensitive. 

```
:local myVar "hello"
# following line will generate error, because variable myVAr is not defined
:put $myVAr
# correct code
:put $myVar
```

Set command without value will un-define the variable (remove from environment, new in v6.2) 

```
#remove variable from environment
:global myVar "myValue"
:set myVar;
```

Use quotes on the full variable name when the name of the variable contains operators. Example: 

```
:local "my-Var";
:set "my-Var" "my value";
:put $"my-Var";
```
