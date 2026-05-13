## Global scope 

Global scope or root scope is the default scope of the script. It is created automatically and can not be turned off. 

**==> picture [13 x 13] intentionally omitted <==**

Previously set global variable can be used in scripts by declaring it without setting the value. 

Local scope 

1094 

User can define their own groups to block access to certain variables, these scopes are called local scopes. Each local scope is enclosed in curly braces ("{ }"). 

```
{
        :local a 3;
        {
                :local b 4;
                :put ($a+$b);
        } #line below will show variable b in light red color since it is not defined in scope
        :put ($a+$b);
}
```

In the code above variable, b has local scope and will not be accessible after a closing curly brace. 

**==> picture [13 x 13] intentionally omitted <==**

Each line written in the terminal is treated as local scope 

So for example, the defined local variable will not be visible in the next command line and will generate a syntax error 

```
[admin@MikroTik] > :local myVar a;
[admin@MikroTik] > :put $myVar
syntax error (line 1 column 7)
```

**==> picture [13 x 12] intentionally omitted <==**

Do not define global variables inside local scopes. 

Note that even variable can be defined as global, it will be available only from its scope unless it is not referenced to be visible outside of the scope. 

```
{
        :local a 3;
        {
                :global b 4;
        }
        :put ($a+$b);
}
```

The code above will output 3, because outside of the scope b is not visible. 

The following code will fix the problem and will output 7: 

```
{
        :local a 3;
        {
                :global b 4;
        }
        :global b;
        :put ($a+$b);
}
```
