## Item Numbers 

Item numbers are assigned by the print command and are not constant - two successive print commands may order items differently. But the results of the last print commands are memorized and, thus, once assigned, item numbers can be used even after add , remove, and move operations. Item numbers are assigned on a per-session basis, they will remain the same until you quit the console or until the next print command is executed. Also, numbers are assigned separately for every item list, so for example, the ip address print will not change the numbering of the interface list. 

It is possible to use item numbers without running the print command. Numbers will be assigned just as if the print command was executed. 

You can specify multiple items as targets for some commands. Almost everywhere, where you can write the number of item, you can also write a list of numbers. 

73 

```
[admin@MikroTik] > interface print
Flags: X - disabled, D - dynamic, R - running
# NAME TYPE MTU
0 R ether1 ether 1500
1 R ether2 ether 1500
2 R ether3 ether 1500
3 R ether4 ether 1500
[admin@MikroTik] > interface set 0,1,2 mtu=1460
[admin@MikroTik] > interface print
 Flags: X - disabled, D - dynamic, R - running
# NAME TYPE MTU
0 R ether1 ether 1460
1 R ether2 ether 1460
2 R ether3 ether 1460
3 R ether4 ether 1500
[admin@MikroTik] >
```

Warning: Do not use Item numbers in scripts, it is not a reliable way to edit items in the scheduler. scripts , etc. Instead, use the "find" command. More info h ere also look at scripting examples.
