## Login Options 

Console login options enable or disable various console features like color, terminal detection, and many other. 

Additional login parameters can be appended to the login name after the '+' sign. 

```
   login_name ::= user_name [ '+' parameters ]
   parameters ::= parameter [ parameters ]
   parameter ::= [ number ] 'a'..'z'
   number ::= '0'..'9' [ number ]
```

If the parameter is not present, then the default value is used. If the number is not present then the implicit value of the parameter is used. 

Example: admin+ct80w - will disable console colors, disable auto detection and then set terminal width to 80. 

**==> picture [253 x 104] intentionally omitted <==**

**----- Start of picture text -----**<br>
Param Default Implicit Description<br>"w" auto auto Set terminal width<br>"h" auto auto Set terminal height<br>"c" on off disable/enable console colors<br>"t" off off Disable auto-detection of terminal capabilities<br>"e" on off Enables "dumb" terminal mode<br>**----- End of picture text -----**<br>
