## Safe Mode 

It is sometimes possible to change router configuration in a way that will make the router inaccessible (except from the local console). Usually, this is done by accident, but there is no way to undo the last change when the connection to the router is already cut. Safe mode can be used to minimize such risk. 

76 

The "Safe Mode" button in the Winbox GUI allows you to enter Safe Mode, while in the CLI, you can access it by either using the keyboard shortcut F4 or pressing [CTRL]+[X] . To exit without saving the made changes in CLI, hit [CTRL]+[D]. 

```
[admin@MikroTik] ip route>[CTRL]+[X]
[Safe Mode taken]
[admin@MikroTik] ip route<SAFE>
```

**==> picture [504 x 431] intentionally omitted <==**

Message Safe Mode taken is displayed and prompt changes to reflect that session is now in safe mode. All configuration changes that are made (also from other login sessions), while the router is in safe mode, are automatically undone if the safe mode session terminates abnormally. You can see all such changes that will be automatically undone and tagged with an F flag in the system history: 

```
[admin@MikroTik] /ip/route>
[Safe Mode taken]
[admin@MikroTik] /ip/route<SAFE> add
[admin@MikroTik] /ip/route<SAFE> /system/history/print
Flags: U, F - FLOATING-UNDO
Columns: ACTION, BY, POLICY
  ACTION                 BY     POLICY
F route 0.0.0.0/0 added  admin  write
```

77 

Now, if the telnet connection (or WinBox terminal) is cut, then after a while (TCP timeout is 9 minutes) all changes that were made while in safe mode will be undone. Exiting session by [Ctrl]+[D] also undoes all safe mode changes, while /quit does not. 

If another user tries to enter safe mode, he's given the following message: 

```
[admin@MikroTik] >
```

```
Hijacking Safe Mode from someone - unroll/release/don't take it [u/r/d]:
```

- [u] - undoes all safe mode changes, and puts the current session in safe mode. 

- [r] - keeps all current safe mode changes, and puts the current session in a safe mode. The previous owner of safe mode is notified about this: 

```
[admin@MikroTik] ip firewall rule input
```

```
[Safe mode released by another user]
```

[d] - leaves everything as-is. 

If too many changes are made while in safe mode, and there's no room in history to hold them all (currently history keeps up to 100 most recent actions), then the session is automatically put out of the safe mode, and no changes are automatically undone. Thus, it is best to change the configuration in small steps, while in safe mode. Pressing [Ctrl] + [X] twice is an easy way to empty the safe mode action list. 

**==> picture [13 x 13] intentionally omitted <==**

As "Safe Mode" operates within the user's session and stores configuration changes, it will be ignored for commands requiring a reboot, such as resetting configuration or restoring from a backup.
