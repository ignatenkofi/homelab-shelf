## Get file contents 

Using the get command, it is possible to retrieve file contents only from files up to 60KB in size. For accessing contents of larger files, use command read The result is returned as an array. 

For example: 

```
[admin@MikroTik] > :put [/file/get text.txt contents]
123456
[admin@MikroTik] > /file/read file=text.txt offset=2 chunk-size=3
  data: 345
```
