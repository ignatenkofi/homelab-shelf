## Default groups 

There are three default system groups which cannot be deleted: 

```
[admin@MikroTik] > /user group print
```

```
0 name="read" policy=local,telnet,ssh,reboot,read,test,winbox,password,web,sniff,sensitive,api,romon,rest-api,!
ftp,!write,!policy skin=default
```

```
1 name="write" policy=local,telnet,ssh,reboot,read,write,test,winbox,password,web,sniff,sensitive,api,romon,
rest-api,!ftp,!policy skin=default
```

```
2 name="full" policy=local,telnet,ssh,ftp,reboot,read,write,policy,test,winbox,password,web,sniff,sensitive,api,
romon,rest-api skin=default
```

Please note, that even the "read" group includes sensitive, reboot, and other important policies, meaning that this group should not be given to untrusted users. For truly limited groups, make a custom group, defining specific policies. All groups have access to file operations. Exclamation sign '!' just before the policy item name means NOT.
