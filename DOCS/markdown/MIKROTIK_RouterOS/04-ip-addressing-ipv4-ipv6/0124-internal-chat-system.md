## Internal Chat System 

RouterOS console has a built-in internal chat system. This allows remotely located admins to talk to each other directly in RouterOS CLI. To start the conversation prefix the intended message with the # symbol, anyone who is logged in at the time of sending the message will see it. 

```
[admin@MikroTik] > # ready to break internet?
[admin@MikroTik] >
fake_admin: i was born ready
[admin@MikroTik] >
```

```
[fake_admin@MikroTik] >
admin: ready to break internet?
[fake_admin@MikroTik] > # i was born ready
[fake_admin@MikroTik] >
```
