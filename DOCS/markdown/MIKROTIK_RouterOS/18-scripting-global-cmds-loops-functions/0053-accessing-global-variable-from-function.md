## Accessing global variable from function 

Logically you would think that globally defined variables should be accessible in functions too, but that is not really the case. Lets see an example: 

`:global myVar "test" :global myFunc do={ :put "global var=$myVar" } [$myFunc]` Output is: 

```
global var=
```

So obviously global variable is not accessible directly. To make it work we need do declare global variable inside the function: 

`:global myVar "test" :global myFunc do={ :global myVar; :put "global var=$myVar" } [$myFunc]` Output: `global var=test`
