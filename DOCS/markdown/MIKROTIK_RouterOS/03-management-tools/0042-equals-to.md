## equals to: 

```
[admin@MikroTik] > ping 10.0.0.1 count 3 size 100
```

It is possible to complete not only the beginning, but also any distinctive sub-string of a name: if there is no exact match, the console starts looking for words that have string being completed as first letters of a multiple word name, or that simply contain letters of this string in the same order. If a single such word is found, it is completed at the cursor position. For example: 

```
[admin@MikroTik] > interface x[TAB]_
[admin@MikroTik] > interface export _
[admin@MikroTik] > interface mt[TAB]_
[admin@MikroTik] > interface monitor-traffic _
```
