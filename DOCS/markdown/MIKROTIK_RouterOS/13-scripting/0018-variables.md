## Variables 

The scripting language has two types of variables: 

global - accessible from all scripts created by the current user, defined by global keyword; local - accessible only within the current scope, defined by local keyword. 

There can be undefined variables. When a variable is undefined, the parser will try to look for variables set, for example, by DHCP lease-script or Hotspot o n-login 

Every variable, except for built-in RouterOS variables, must be declared before usage by local or global keywords. Undefined variables will be marked as undefined and will result in a compilation error. Example: 

```
# following code will result in compilation error, because myVar is used without declaration
:set myVar "my value";
:put $myVar
```

Correct code: 

```
:local myVar;
:set myVar "my value";
:put $myVar;
```

The exception is when using variables set, for example, by DHCP lease-script 

```
/system script
add name=myLeaseScript policy=\
        ftp,reboot,read,write,policy,test,winbox,password,sniff,sensitive,api \
        source=":log info \$leaseActIP\r\
        \n:log info \$leaseActMAC\r\
        \n:log info \$leaseServerName\r\
        \n:log info \$leaseBound"
```

```
/ip dhcp-server set myServer lease-script=myLeaseScript
```

1099 

Valid characters in variable names are letters and digits. If the variable name contains any other character, then the variable name should be put in double quotes. Example: 

```
#valid variable name
:local myVar;
#invalid variable name
:local my-var;
#valid because double quoted
:global "my-var";
```

If a variable is initially defined without value then the variable data type is set to nil, otherwise, a data type is determined automatically by the scripting engine. Sometimes conversion from one data type to another is required. It can be achieved using data conversion commands. Example: `#convert string to array :local myStr "1,2,3,4,5"; :put [:typeof $myStr]; :local myArr [:toarray $myStr]; :put [:typeof $myArr]`
