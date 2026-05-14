## Retrieve information 

The command will return two values: 

exit-code : returns 0 if the command execution succeeded output : returns the output of remotely executed command 

Example: Code below will retrieve interface status of ether1 from device 10.10.10.1 and output the result to "Log" 

```
:local Status ([/system ssh-exec address=10.10.10.1 user=remote command=":put ([/interface ethernet monitor
[find where name=ether1] once as-value]->\"status\")" as-value]->"output")
:log info $Status
```

**==> picture [13 x 13] intentionally omitted <==**

For security reasons you should not use plain text password with parameter "password" specified in the command line. To ensure safe execution of the command remotely, it is strongly recommended to use SSH PKI authentication for users on both sides. 

**==> picture [13 x 13] intentionally omitted <==**

The user group and script policy executing the command requires test permission 

Watch how to execute commands through SSH. 

246
