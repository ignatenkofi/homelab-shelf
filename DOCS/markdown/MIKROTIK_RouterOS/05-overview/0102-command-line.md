## Command Line 

It is possible to use the command line to pass connect to, user, password and session ("workspace" for WInBox 4) parameters automatically: 

```
winbox.exe [<connect-to> [<login> [<password>]] <session|workspace>]
```

For example (with no password): 

```
winbox.exe 10.5.101.1 admin "" "<own>"
```

Will connect to router 10.5.101.1 with user "admin" without a password and use session|workspace "<own>". 

It is possible to use the command line to pass connect to, user, and password parameters automatically to connect to the router through RoMON. In this case, RoMON Agent must be saved on the Managed routers list so WinBox would know the user and password for this device: 

```
winbox.exe --romon [<romon-agent> [<connect-to> [<login> [<password>]]] <session|workspace>]
```

For example (with no password): 

```
winbox.exe --romon 10.5.101.1 D4:CA:6D:E1:B5:7D admin "" "<own>"
```

Will connect to router D4:CA:6D:E1:B5:7D, through 10.5.101.1 via RoMON Agent with user "admin" without a password and apply session|workspace called "<own>".
