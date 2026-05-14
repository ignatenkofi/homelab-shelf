## Concatenation Operators 

**==> picture [422 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Operator Description Example<br>"." concatenates two strings :put ("concatenate" . " " . "string");<br>"," concatenates two arrays or adds an element to the array :put ({1;2;3} , 5 );<br>**----- End of picture text -----**<br>

It is possible to add variable values to strings without a concatenation operator: 

```
:global myVar "world";
```

```
:put ("Hello " . $myVar);
# next line does the same as above
:put "Hello $myVar";
```

By using $[] and $() in the string it is possible to add expressions inside strings: 

1098 

```
:local a 5;
:local b 6;
:put " 5x6 = $($a * $b)";
:put " We have $[ :len [/ip route find] ] routes";
```
