## Configuration Undo and Redo 

Any action done in the GUI or any command executed from the CLI is recorded in `/system history` .  You can undo or redo any action by running undo or redo commands from the CLI or by clicking on Undo, and Redo buttons from the GUI. 

A simple example to demonstrate the addition of the firewall rule and how to undo and redo the action: 

```
[admin@v7_ccr_bgp] /ip/firewall/filter> add chain=forward action=drop
```

```
[admin@v7_ccr_bgp] /ip/firewall/filter> print
Flags: X - disabled, I - invalid; D - dynamic
0 X chain=input action=drop protocol=icmp src-address=10.155.101.1 log=no
log-prefix=""
```

```
1 chain=forward action=drop
[admin@v7_ccr_bgp] /ip/firewall/filter> /system/history/print
Flags: U - undoable, R - redoable, F - floating-undo
Columns: ACTION, BY, POLICy
ACTION BY POLIC
F filter rule added admin write
U --- write
[admin@v7_ccr_bgp] /ip/firewall/filter>
```

We have added a firewall rule and in `/system history` we can see all that was done. 

Let's undo everything: 

```
[admin@v7_ccr_bgp] /ip/firewall/filter> /undo
[admin@v7_ccr_bgp] /ip/firewall/filter> print
Flags: X - disabled, I - invalid; D - dynamic
0 X chain=input action=drop protocol=icmp src-address=10.155.101.1 log=no
log-prefix=""
```

```
[admin@v7_ccr_bgp] /ip/firewall/filter>
```

As you can see firewall rule disappeared. Now redo the last change: 

55 

```
[admin@v7_ccr_bgp] /ip/firewall/filter> /redo
[admin@v7_ccr_bgp] /ip/firewall/filter> print
Flags: X - disabled, I - invalid; D - dynamic
0 X chain=input action=drop protocol=icmp src-address=10.155.101.1 log=no
log-prefix=""
```

```
1 chain=forward action=drop
```

```
[admin@v7_ccr_bgp] /ip/firewall/filter>
```

System history is capable of showing exact CLI commands that will be executed during "Undo" or "Redo" actions even if we perform the action from GUI, for example, detailed history output after adding TCP accept rule from WinBox: 

```
[admin@v7_ccr_bgp] /system/history> print detail
Flags: U - undoable, R - redoable, F - floating-undo
 F redo=
      /ip firewall filter add action=accept chain=forward disabled=no log=no \
          log-prefix="" protocol=tcp
    undo=/ip firewall filter remove *4 action="filter rule added" by="admin"
    policy=write time=oct/10/2019 18:51:05
 F redo=/ip firewall filter add action=accept chain=forward
    undo=/ip firewall filter remove *3 action="filter rule added" by="admin"
    policy=write time=oct/10/2019 18:49:03
U redo="" undo="" action="---" by="" policy=write time=sep/27/2019 13:07:35
[admin@v7_ccr_bgp] /system/history>
```
