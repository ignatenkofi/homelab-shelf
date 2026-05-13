## Return example 

```
:global myFunc do={ :return ($a + $b)}
:put [$myFunc a=6 b=2]
output:
8
```

You can even clone an existing script from the script environment and use it as a function. 

```
#add script
/system script add name=myScript source=":put \"Hello \$myVar !\""
```

```
:global myFunc [:parse [/system script get myScript source]]
$myFunc myVar=world
```

```
output:
Hello world !
```

**==> picture [13 x 13] intentionally omitted <==**

If the function contains a defined global variable that names match the name of the passed parameter, then the globally defined variable is ignored, for compatibility with scripts written for older versions. This feature can change in future versions. Avoid using parameters with the same name as global variables.
