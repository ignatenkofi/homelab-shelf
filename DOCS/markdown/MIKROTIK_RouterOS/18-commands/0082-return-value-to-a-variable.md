## Return value to a variable 

It is possible to save the result of the fetch command to a variable. For example, it is possible to trigger a certain action based on the result that an HTTP page returns. You can find a very simple example below that disables ether2 whenever a PHP page returns "0": 

```
{
```

```
    :local result [/tool fetch url=https://10.0.0.1/disable_ether2.php as-value output=user];
```

```
    :if ($result->"status" = "finished") do={
```

```
        :if ($result->"data" = "0") do={
```

```
            /interface ethernet set ether2 disabled=yes;
```

```
        } else={
            /interface ethernet set ether2 disabled=no;
        }
    }
}
```

1141
