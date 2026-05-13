## Interface Overview 

WinBox interface has been designed to be intuitive for most of the users. The interface consists of: 

The main toolbar at the top where users can add various info fields, like CPU and memory usage. 

The menu bar on the left - list of all available menus and sub-menus. This list changes depending on what packages are installed. For example, if the IPv6 package is disabled, then the IPv6 menu and all its sub-menus will not be displayed. Work area - an area where all menu windows are opened. 

**==> picture [504 x 367] intentionally omitted <==**

The title bar shows information to identify with which router WinBox session is opened. Information is displayed in the following format: 

```
[username]@[Router's IP or MAC] ( [RouterID] ) - WinBox [ROS version] on [RB model] ([platform])
```

From screenshot above we can see that user krisjanis is logged into router with IPv4/IPv6 address [fe80::4e5e:cff:fef6:c0ab%3] . Router's ID is 3C18Krisjanis_GW , currently installed RouterOS version is v6.36rc6 , RouterBoard is CCR1036-12G-4S and platform is tile . 

On the Main toolbar's left side is located: 

262 

undo redo Safe Mode Currently loaded session 

More about Safe mode and undoing performed actions read in this article. 

On the right side is located: 

an indicator that shows whether the WinBox session uses encryption WinBox traffic indicator displayed as a green bar, 

Custom info fields that can be added by the user by right-clicking on the toolbar and picking available info fields from the list
