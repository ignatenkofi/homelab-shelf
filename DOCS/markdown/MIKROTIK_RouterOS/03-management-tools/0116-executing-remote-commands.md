## Executing remote commands 

To execute remote command it has to be supplied at the end of log-in line 

```
/system ssh 192.168.88.1 "/ip address print"
/system ssh 192.168.88.1 command="/ip address print"
/system ssh 2001:db8:add:1337::beef "/ip address print"
/system ssh 2001:db8:add:1337::beef command="/ip address print"
```

**==> picture [13 x 13] intentionally omitted <==**

If the server does not support pseudo-tty (ssh -T or ssh host command), like MikroTik ssh server, then it is not possible to send multiline commands via SSH 

For example, sending command `"/ip address \n add address=1.1.1.1/24"` to MikroTik router will fail. 

**==> picture [13 x 13] intentionally omitted <==**

If you wish to execute remote commands via scripts or scheduler , use command ssh-exec .
