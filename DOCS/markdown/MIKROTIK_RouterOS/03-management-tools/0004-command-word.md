## Command word 

The first word in the sentence has to be a command followed by attribute words and a zero-length word or terminating word. The name of the command word should begin with '/'. Names of commands closely follow CLI, with spaces replaced with '/'. Some commands are specific to API; 

Command word structure in the strict order: 

encoded length content prefix / CLI converted command 

API-specific commands: 

```
login
cancel
```

Command word content examples: 

```
/login
```

```
/user/active/listen
```

- `/interface/vlan/remove` 

```
/system/reboot
```
