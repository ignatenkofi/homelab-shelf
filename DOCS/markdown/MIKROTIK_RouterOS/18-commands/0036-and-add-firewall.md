## and add firewall 

```
/ip firewall filter
```

```
add chain=forward dst-address-list=restricted action=drop
```

Now we can write a script and schedule it to run, let's say, every 30 seconds. 

Script Code: 

1117 

```
:foreach i in=[/ip dns cache find] do={
    :local bNew "true";
    :local cacheName [/ip dns cache all get $i name] ;
#    :put $cacheName;
    :if (([:find $cacheName "rapidshare"] >= 0) || ([:find $cacheName "youtube"] >= 0)) do={
        :local tmpAddress [/ip dns cache get $i address] ;
#        :put $tmpAddress;
# if address list is empty do not check
        :if ( [/ip firewall address-list find list="restricted" ] = "") do={
            :log info ("added entry: $[/ip dns cache get $i name] IP $tmpAddress");
            /ip firewall address-list add address=$tmpAddress list=restricted comment=$cacheName;
        } else={
            :foreach j in=[/ip firewall address-list find list="restricted"] do={
                :if ( [/ip firewall address-list get $j address] = $tmpAddress ) do={
                    :set bNew "false";
                }
            }
            :if ( $bNew = "true" ) do={
                :log info ("added entry: $[/ip dns cache get $i name] IP $tmpAddress");
                /ip firewall address-list add address=$tmpAddress list=restricted comment=$cacheName;
            }
        }
    }
}
```
