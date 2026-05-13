## Relational Operators 

**==> picture [166 x 137] intentionally omitted <==**

**----- Start of picture text -----**<br>
Operator Description Example<br>"<" less :put (3<4);<br>">" greater :put (3>4);<br>"=" equal :put (2=2);<br>"<=" less or equal<br>">=" greater or equal<br>"!=" not equal<br>**----- End of picture text -----**<br>


To negate an expression, you can use "expression=false". To print all interfaces that are not "ethernet", you can use expression negation like this: 

```
/interface/print where (name~"ether")=false
```

Or to do the opposite, you can use "expression=true": 

```
/interface/print where (name~"ether")=true
```
