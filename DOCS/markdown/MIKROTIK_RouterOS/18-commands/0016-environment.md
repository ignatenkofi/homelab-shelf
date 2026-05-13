## Environment 

Sub-menu level: 

```
/system script environment
/environment
```

Contains all user-defined variables and their assigned values. 

```
[admin@MikroTik] > :global example;
[admin@MikroTik] > :set example 123
[admin@MikroTik] > /environment print
"example"=123
```

Read-only status properties: 

**==> picture [170 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string) Variable name<br>user  (string) The user who defined variable<br>value  () The value assigned to a variable<br>**----- End of picture text -----**<br>
