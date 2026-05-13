## Special Login 

Special login can be used to access another device (like a switch, for example) that is connected through a serial cable by opening a telnet/ssh session that will get you directly on this device (without having to login to RouterOS first). 

For demonstration we will use two RouterBoards and one PC. 

240 

**==> picture [505 x 122] intentionally omitted <==**

Routers R1 and R2 are connected with serial cable and PC is connected to R1 via ethernet. Lets say we want to access router R2 via serial cable from our PC. To do this you have to set up serial interface proxy on R1. It can be done by feature called special-login . 

**==> picture [13 x 13] intentionally omitted <==**

By default console is bound to serial port. 

First task is to unbind console from serial simply by disabling entry in /system console menu: 

```
[admin@MikroTik] /system console> print
Flags: X - disabled, U - used, F - free
 #   PORT                                                                    TERM
 0 X serial0                                                                 vt102
```

Next step is to add new user, in this case serial, and bind it to the serial port 

```
[admin@MikroTik] > /user add name=serial group=full
[admin@MikroTik] > /special-login add user=serial port=serial0 disabled=no
[admin@MikroTik] > /special-login print
Flags: X - disabled
 #   USER                                                                    PORT
 0   serial                                                                  serial0
```

Now we are ready to access R2 from our PC. 

```
maris@bumba:/$ ssh serial@10.1.101.146
[Ctrl-A is the prefix key]
R2 4.0beta4
R2 Login:
[admin@R2] >
```

To exit special login mode press Ctrl+A and Q 

```
[admin@MikroTik] >
[Q - quit connection]      [B - send break]
[A - send Ctrl-A prefix]   [R - autoconfigure rate]
Connection to 10.1.101.146 closed.
```

**==> picture [13 x 13] intentionally omitted <==**

After router reboot and serial cable attached router may stuck at Bootloader main menu 

To fix this problem you need to allow access bootloader main menu from <any> key to <delete>: 

241 

enter bootloader menu press 'k' for boot key options press '2' to change key to <delete> 

```
What do you want to configure?
d - boot delay
k - boot key
s - serial console
n - silent boot
o - boot device
u - cpu mode
f - cpu frequency
r - reset booter configuration
e - format nand
g - upgrade firmware
i - board info
p - boot protocol
b - booter options
t - call debug code
l - erase license
x - exit setup
your choice: k - boot key
```

```
Select key which will enter setup on boot:
* 1 - any key
  2 - <Delete> key only
```

```
your choice: 2
```

242
