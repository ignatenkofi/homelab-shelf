## Queries 

The print command accepts query words that limit the set of returned sentences. 

Query words begin with '?'. 

The order of query words is significant. A query is evaluated starting from the first word. 

- A query is evaluated for each item in the list. If the query succeeds, the item is processed, if a query fails, the item is ignored. 

- A query is evaluated using a stack of boolean values. Initially, the stack contains an infinite amount of 'true' values. At the end of the evaluation, if the stack contains at least one 'false' value, the query fails. 

- Query words operate according to the following rules: 

**==> picture [516 x 270] intentionally omitted <==**

**----- Start of picture text -----**<br>
Query Description<br>?name pushes 'true' if an item has a value of property name, 'false' if it does not.<br>?-name pushes 'true' if an item does not have a value of property name, 'false' otherwise.<br>?name=x pushes 'true' if the property name has a value equal to , 'false' otherwise.x<br>?=name=x<br>?<name=x pushes 'true' if the property name has a value less than , 'false' otherwise.x<br>?>name=x pushes 'true' if the property name has a value greater than , 'false' otherwise.x<br>?#operations applies operations to the values in the stack.<br>operation string is evaluated from left to right.<br>the sequence of decimal digits followed by any other character or end of the word is interpreted as a stack index. top value has an<br>index 0.<br>an index that is followed by a character pushes a copy of the value at that index.<br>an index that is followed by the end of the word replaces all values with the value at that index.<br>!  character replaces the top value with the opposite.<br>&  pops two values and pushes the result of logical 'and' operation.<br>|  pops two values and pushes the result of logical 'or' operation.<br>.  after an index does nothing.<br>.  after another character pushes a copy of the top value.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

Regular expressions are not supported in API, so do not try to send a query with the  symbol ~ 

Examples: 

Get all ethernet and VLAN interfaces: 

```
/interface/print
?type=ether
```

```
?type=vlan
```

```
?#|
```

Get all routes that have a non-empty comment: 

```
/ip/route/print
```

```
?>comment=
```

199 

Forum thread with a detailed explanation of the use of queries
