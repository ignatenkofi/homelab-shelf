## Command Prompt 

At the end of the successful login sequence, the login process prints a banner that shows the command prompt, and hands over control to the user. 

Default command prompt consists of user name, system identity, and current command path /> 

For example, change the current path from the root to the interface then go back to the root 

```
  [admin@MikroTik] > interface [enter]
  [admin@MikroTik] /interface> / [enter]
  [admin@MikroTik] >
```

Use up arrow to recall previous commands (if this is a multiline command, then you can press F8 in order to expand it) from command history (commands that added sensitive data, like passwords, will not be available in the history), TAB key to automatically complete words in the command you are typing, EN TER key to execute the command, Control-C to interrupt currently running command and return to prompt and ? to display built-in help, in RouterOS v7 , F1 has to be used instead. 

213 

The easiest way to log out of the console is to press Control-D at the command prompt while the command line is empty (You can cancel the current command and get an empty line with Control-C , so Control-C followed by Control-D will log you out in most cases). 

It is possible to write commands that consist of multiple lines. When the entered line is not a complete command and more input is expected, the console shows a continuation prompt that lists all open parentheses, braces, brackets, and quotes, and also trailing backslash if the previous line ended with backsl ash -white-space. 

```
    [admin@MikroTik] > {
    {... :put (\
    {(\... 1+2)}
    3
```

When you are editing such multiple line entries, the prompt shows the number of current lines and total line count instead of the usual username and system name. 

```
line 2 of 3> :put (\
```

Sometimes commands ask for additional input from the user. For example, the command ' `/password` ' asks for old and new passwords. In such cases, the prompt shows the name of the requested value, followed by colon and space. 

```
    [admin@MikroTik] > /password
    old password: ******
    new password: **********
    retype new password: **********
```
