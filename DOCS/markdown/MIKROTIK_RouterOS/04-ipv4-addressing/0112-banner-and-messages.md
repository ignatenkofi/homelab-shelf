## Banner and Messages 

The login process will display the MikroTik banner and short help after validating the user name and password. 

212 

```
  MMM      MMM       KKK                          TTTTTTTTTTT      KKK
  MMMM    MMMM       KKK                          TTTTTTTTTTT      KKK
  MMM MMMM MMM  III  KKK  KKK  RRRRRR     OOOOOO      TTT     III  KKK  KKK
  MMM  MM  MMM  III  KKKKK     RRR  RRR  OOO  OOO     TTT     III  KKKKK
  MMM      MMM  III  KKK KKK   RRRRRR    OOO  OOO     TTT     III  KKK KKK
  MMM      MMM  III  KKK  KKK  RRR  RRR   OOOOOO      TTT     III  KKK  KKK
  MikroTik RouterOS 6.22 (c) 1999-2014       https://www.mikrotik.com/
```

```
[?]             Gives the list of available commands
command [?]     Gives help on the command and list of arguments
```

```
[Tab]           Completes the command/word. If the input is ambiguous,
                a second [Tab] gives possible options
```

```
/               Move up to base level
..              Move up one level
/command        Use command at the base level
```

After the banner can be printed other important information, like /system note set by another admin, the last few critical log messages, demo version upgrade reminder, and default configuration description. 

For example, the demo license prompt and last critical messages are printed 

```
UPGRADE NOW FOR FULL SUPPORT
----------------------------
FULL SUPPORT benefits:
- receive technical support
- one year feature support
- one year online upgrades
    (avoid re-installation and re-configuring your router)
To upgrade, register your license "software ID"
on our account server www.mikrotik.com
```

```
Current installation "software ID": ABCD-456
```

```
Please press "Enter" to continue!
```

```
dec/10/2007 10:40:06 system,error,critical login failure for user root from 10.0.0.1 via telnet
dec/10/2007 10:40:07 system,error,critical login failure for user root from 10.0.0.1 via telnet
dec/10/2007 10:40:09 system,error,critical login failure for user test from 10.0.0.1 via telnet
```
