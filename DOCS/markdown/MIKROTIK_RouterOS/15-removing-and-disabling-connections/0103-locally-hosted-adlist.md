## Locally hosted adlist: 

To create your adlist, you can create a Txt file with the domains. Example: 

```
0.0.0.0 example1.com
0.0.0.0 eu1.example.com
0.0.0.0 ex.com
0.0.0.0 com.example.com
```

**==> picture [13 x 13] intentionally omitted <==**

You can create the txt file on your PC, but it is also possible to create it in RouterOS, with following commands 

"/file/add name=host.txt", and then you can run "file/edit host.txt contents" after adding entries, press "ctrl o" to save the entries. 

To add file to adlist : 

921 

```
/ip/dns/adlist/add file=host.txt
```

**==> picture [13 x 12] intentionally omitted <==**

You can verify that file is formatted correctly with "/ip/dns/adlist/print" ,the results will show how many hostnames you have added, the hostname format must match the format given in previous example. 

```
/ip/dns/adlist/print
Flags: X - disabled
 0   file=host.txt match-count=0 name-count=4
```
