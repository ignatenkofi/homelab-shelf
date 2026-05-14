## One-click login 

It is possible to create a modified captive portal for quick one-click login for scenarios where no user or password is required. 

What you need to do is: 

Create a user for this purpose. In example, it is "notsosecretuser" with password "notsosecretpass" Assign this user to a user profile that allows a specific/unlimited amount of simultaneous active users. Copy original hotspot directory that is already generated in routers file menu on root level. Modify the contents of this copy directory contents. 

Only one file requires modifications for this to work, the "login.html". 

Original: 

```
<table width="100" style="background-color: #ffffff">
```

- `<tr><td align="right">login</td>` 

- `<td><input style="width: 80px" name="username" type="text" value="$(username)"/></td> </tr>` 

- `<tr><td align="right">password</td>` 

- `<td><input style="width: 80px" name="password" type="password"/></td> </tr>` 

- `<tr><td> </td>` 

- `<td><input type="submit" value="OK" /></td> </tr>` 

- `</table>` 

Modified: 

303 

```
<table width="100" style="background-color: #ffffff">
```

```
  <tr style="display:none;"><td align="right">login</td>
```

- `<td><input style="width: 80px" name="username" type="text" value="notsosecretuser"/></td> </tr>` 

```
  <tr style="display:none;"><td align="right">password</td>
```

- `<td><input style="width: 80px" name="password" type="password" value="notsosecretpass"/></td> </tr>` 

- `<tr><td> </td>` 

- `<td><input type="submit" value="Proceed to Internet!" /></td>` 

- `</tr>` 

```
</table>
```

What changed: 

User and Password "" fields are hidden. Both User and Password field values contain predefined values. Changed the "OK" button value(name) to something more fitting. 

Now upload this new hotspot folder back to the router, preferably with a different name. Change settings in the hotspot server profile to use this new html directory. 

```
/ip hotspot profile set (profile number or name) html-directory-override=(dir path/name)
```
