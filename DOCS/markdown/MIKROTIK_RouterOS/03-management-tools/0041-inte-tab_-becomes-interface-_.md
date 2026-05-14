## /inte [Tab]_ becomes /interface _ 

If there is more than one match, but they all have a common beginning, which is longer than that what you have typed, then the word is completed to this common part, and no space is appended: 

/interface set e [Tab]_ becomes /interface set ether_ 

If you've typed just the common part, pressing the tab key once has no effect. However, pressing it for the second time shows all possible completions in compact form: 

217 

```
[admin@MikroTik] > interface set e[Tab]_
[admin@MikroTik] > interface set ether[Tab]_
[admin@MikroTik] > interface set ether[Tab]_
ether1 ether5
[admin@MikroTik] > interface set ether_
```

The [Tab] key can be used almost in any context where the console might have a clue about possible values - command names, argument names, arguments that have only several possible values (like names of items in some lists or name of the protocol in firewall and NAT rules). You cannot complete numbers, IP addresses, and similar values. 

Another way to press fewer keys while typing is to abbreviate command and argument names. You can type only the beginning of the command name, and, if it is not ambiguous, the console will accept it as a full name. So typing: 

```
[admin@MikroTik] > pi 10.1 c 3 si 100
```
