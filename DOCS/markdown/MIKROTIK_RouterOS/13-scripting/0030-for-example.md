## For example: 

```
:global my2 "123"
```

```
:global myFunc do={ :global my2; :put $my2; :set my2 "lala"; :put $my2 }
$myFunc my2=1234
:put "global value $my2"
```

The output will be: 

```
1234
lala
global value 123
```

Nested function example 

Note: to call another function its name needs to be declared (the same as for variables) 

1108 

```
:global funcA do={ :return 5 }
:global funcB do={
        :global funcA;
        :return ([$funcA] + 4)
}
:put [$funcB]
Output:
9
```
