## How to remove variables 

You could use `/system script environment remove` to remove unused variables, however more preferred method is to unset variable. 

Setting no value to existing parameter will unset it, see example below: 

```
[admin@MikroTik] /system script environment> :global myVar 1
[admin@MikroTik] /system script environment> print
# NAME               VALUE
0 myVar              1
[admin@MikroTik] /system script environment> :set myVar
[admin@MikroTik] /system script environment> print
# NAME               VALUE
[admin@MikroTik] /system script environment>
```
