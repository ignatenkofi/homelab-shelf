## Filter Syntax 

The routing filter rule implements script-like syntax. The example below is a quick demonstration of a routing filter that matches prefixes with a prefix length greater than 24 from subnet 192.168.1.0/24 and increments the default distance by 1. If there is no match then subtract the default distance by one. 

```
/routing filter rule
  add chain=myChain \
```

```
  rule="if (dst in 192.168.1.0/24 && dst-len>24) {set distance +1; accept} else {set distance -1; accept}"
```

Filter rule may consist of multiple matchers and actions: 

```
if ( [matchers] ) { [actions] } else { [actions] }
```

There are two types of properties: 

only readable - ones that value is only readable and cannot be rewritten, these properties can be used only by matchers readable/writable - ones that value is readable and writeable, used by filter actions, and also can be used by matchers 

Readable properties can be matched by other readable properties (for numeric properties only) or constant values using boolean operators. 

```
[matchers]:
[prop readable] [bool operator] [prop readable]
```

```
[actions]:
[action] [prop writeable] [value]
```

The boolean operator is not used if there is only one possible operation. 

Example without boolean operator: 

```
if ( protocol connected ) { accept }
```

1054 

Example with boolean operator: 

```
if ( bgp-med < 30 ) { accept }
```

With readable flag properties, matcher is used without specified boolean operator and without value 

```
if ( ospf-dn ) { reject }
```

**==> picture [13 x 13] intentionally omitted <==**

Be aware that the default action of the routing filter chain is "reject"
