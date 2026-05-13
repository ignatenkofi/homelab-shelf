## equals to: 

```
[admin@MikroTik] > ping 10.0.0.1 count 3 size 100
```

It is possible to complete not only the beginning, but also any distinctive substring of a name: if there is no exact match, the console starts looking for words that have string being completed as first letters of a multiple-word name, or that simply contain letters of this string in the same order. If a single such word is found, it is completed at the cursor position. For example: 

74 

```
[admin@MikroTik] > interface x[TAB][TAB]_
dot1x  vxlan  export
[admin@MikroTik] > interface mt[TAB]_
```

```
[admin@MikroTik] > interface monitor-traffic _
```
