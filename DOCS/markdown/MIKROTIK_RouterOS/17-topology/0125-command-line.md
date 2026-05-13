## Command-line 

The RouterOS console uses the following command syntax: 

- `[prefix] [path] command [uparam] [param=[value]] .. [param=[value]]` 

   - [prefix] - ":" or "/" character which indicates if a command is ICE or path. It may not be required. 

   - [path] - relative path to the desired menu level. It may not be required. command - one of the commands available at the specified menu level. 

   - [uparam] - unnamed parameter, must be specified if the command requires it. 

   - [params] - a sequence of named parameters followed by respective values 

The end of the command line is represented by the token “;” or NEWLINE. Sometimes “;” or NEWLINE is not required to end the command line. 

Single command inside `(), [] or {}` does not require any end-of-command character. The end of the command is determined by the content of the whole script 

```
:if ( true ) do={ :put "lala" }
```

Each command line inside another command line starts and ends with square brackets "[ ]" (command concatenation). 

```
:put [/ip route get [find gateway=1.1.1.1]];
```

Notice that the code above contains three command lines: 

:put /ip route get find gateway=1.1.1.1 

Command-line can be constructed from more than one physical line by following line joining rules.
