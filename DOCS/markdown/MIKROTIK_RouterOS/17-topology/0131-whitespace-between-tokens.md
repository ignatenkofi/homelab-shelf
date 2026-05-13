## Whitespace between tokens 

Whitespace can be used to separate tokens. Whitespace is necessary between two tokens only if their concatenation could be interpreted as a different token. Example: 

```
{
        :local a true; :local b false;
# whitespace is not required
        :put (a&&b);
# whitespace is required
        :put (a and b);
}
```

Whitespace characters are not allowed 

between '<parameter>=' 

between 'from=' 'to=' 'step=' 'in=' 'do=' 'else='
