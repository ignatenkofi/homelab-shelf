## Functions 

Scripting language does not allow you to create functions directly, however, you could use :parse command as a workaround. 

Starting from v6.2 new syntax is added to easier define such functions and even pass parameters. It is also possible to return function value with :return co mmand. 

See examples below: 

1107 

```
#define function and run it
:global myFunc do={:put "hello from function"}
$myFunc
output:
hello from function
#pass arguments to the function
:global myFunc do={:put "arg a=$a"; :put "arg '1'=$1"}
$myFunc a="this is arg a value" "this is arg1 value"
```

```
output:
arg a=this is arg a value
arg '1'=this is arg1 value
```

Notice that there are two ways how to pass arguments: 

pass arg with a specific name ("a" in our example) pass value without arg name, in such case arg "1", "2" .. "n" is used.
