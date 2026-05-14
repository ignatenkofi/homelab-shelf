## Conditional statement 

**==> picture [509 x 53] intentionally omitted <==**

**----- Start of picture text -----**<br>
Command Syntax Description<br>if :if (<condition>) do={<commands>}  If a given condition is true then execute commands in the do block, otherwise<br>else={<commands>} execute commands in the else block if specified.<br>**----- End of picture text -----**<br>

Example: 

```
{
        :local myBool true;
        :if ($myBool = false) do={ :put "value is false" } else={ :put "value is true" }
}
```
