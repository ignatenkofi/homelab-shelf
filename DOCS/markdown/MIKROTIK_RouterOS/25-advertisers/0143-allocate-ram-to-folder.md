## Allocate RAM to folder 

It is possible to add folders linked to RAM. Folders will be emptied on reboot or power loss. RAM will be filled up to tmpfs-max-size and if this variable in not provided - up to 1/2 from available RAM. 

1664 

```
[admin@MikroTik] >  /disk add type=tmpfs tmpfs-max-size=100M
[admin@MikroTik] > file print
Columns: NAME, TYPE, SIZE, CREATION-TIME
#  NAME            TYPE       SIZE             CREATION-TIME
0  tmp1             disk     100 003 840        dec/12/2022 11:01:48
```
