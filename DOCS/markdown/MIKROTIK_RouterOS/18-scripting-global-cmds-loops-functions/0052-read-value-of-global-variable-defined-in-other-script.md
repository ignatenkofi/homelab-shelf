## Read value of global variable defined in other script 

Lets say we have one script that declares variable and sets the value: 

```
/system script add name=script1 source={
 :global myVar "hello!"
}
```

And we want to write the value of that variable in log from another script. Simply adding `/log info $myVar` will fail to return correct value, because second script does not know anything about variables defined in another scripts. To make it work properly variable need to be defined, so correct second script code is: 

```
/system script add name=script2 source={
 :global myVar;
 :log info "value is: $myvar"
}
```
