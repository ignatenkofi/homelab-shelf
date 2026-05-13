## Reserved variable names 

All built-in RouterOS properties are reserved variables. Variables that will be defined the same as the RouterOS built-in properties can cause errors. To avoid such errors, use custom designations. 

For example, the following script will not work: 

```
{
:local type "ether1";
/interface print where name=$type;
}
```

But will work with different defined variables: 

```
 {
:local customname "ether1";
/interface print where name=$customname;
}
```

1100
