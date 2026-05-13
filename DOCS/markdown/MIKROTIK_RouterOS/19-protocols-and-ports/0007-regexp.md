## Regexp 

Req-filename field allowed regexp, allowed regexp in this field are: 

brackets () - marking subsection: 

```
    example 1 a(sd|fg) will match asd or afg
```

asterisk "*" - match zero or more times preceding symbol: 

```
    example 1 a* will match any length name consisting purely of symbols  or no symbols at alla
    example 2 .* will match any length name, also, empty field
    example 3 as*df will match adf, asdf, assdf, asssdf etc.
```

plus "+" will match one or more times the preceding symbol: 

```
    example: as+df will match asdf, assdf etc.
```

dot "." - matches any symbol: 

```
    example as.f will match asdf, asbf ashf etc.
```

square brackets [] - variation between: 

```
    example as[df] will match asd and asf
```

question mark "?" will match one or no symbols: 

```
    example asd?f will match asdf and asf
```

caret "^" - used at the beginning of the line means that the line starts with; 

dollar "$" - means at the end of the line.
