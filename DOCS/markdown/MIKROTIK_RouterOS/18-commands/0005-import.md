## import 

The import command is available from the root menu and is used to import configuration from files created by an export command or written manually by hand. 

Starting from 7.16.x version, its possible to catch syntax errors: 

```
[admin@admin] > do { import test.rsc } on-error={ :put "Failure" }
Failure
```

New parameter onerror can be used: 

```
[admin@admin] > onerror e in={ import test.rsc } do={ :put "Failure - $e" }
Failure - Script Error: bad command name this (line 1 column 1)
```

In addition, the import command has new options in verbose mode - the dry-run parameter is specially designed for debugging and can find multiple errors without changing the configuration. 

```
[admin@admin] > import test.rsc verbose=yes dry-run
#line 1
this
bad command name this (line 1 column 1)
...
Script Error: found 5 error(s) in import file
```
