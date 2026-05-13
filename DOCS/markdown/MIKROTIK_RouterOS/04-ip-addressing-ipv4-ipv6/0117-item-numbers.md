## Item Numbers 

215 

Item numbers are assigned by the print command and are not constant - it is possible that two successive print commands will order items differently. But the results of the last print commands are memorized and, thus, once assigned, item numbers can be used even after add, remove and move operations (since version 3, move operation does not renumber items). Item numbers are assigned on a per session basis, they will remain the same until you quit the console or until the next print command is executed. Also, numbers are assigned separately for every item list, so / `ip address print` will not change the numbering of the interface list. 

You can specify multiple items as targets to some commands. Almost everywhere, where you can write the number of items, you can also write a list of numbers. 

```
[admin@MikroTik] > interface print
Flags: X - disabled, D - dynamic, R - running
  #    NAME                 TYPE             MTU
  0  R ether1               ether            1500
  1  R ether2               ether            1500
  2  R ether3               ether            1500
  3  R ether4               ether            1500
[admin@MikroTik] > interface set 0,1,2 mtu=1460
[admin@MikroTik] > interface print
Flags: X - disabled, D - dynamic, R - running
  #    NAME                 TYPE             MTU
  0  R ether1               ether            1460
  1  R ether2               ether            1460
  2  R ether3               ether            1460
  3  R ether4               ether            1500
[admin@MikroTik] >
```
