## Properties 

**==> picture [516 x 202] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IPv6 ad IPv6 address.  Address can also be constructed from the pool if  from-pool  property is specified.<br>dress [IPv6] /  For example if address is set to ::1/64 then address will be constructed as follows <prefix_from_pool>::1/64<br>netmask [0..128];<br>Default: )<br>advertise  (yes |  Whether to enable stateless address configuration. The prefix of that address is automatically advertised three times to hosts using<br>no; Default:  no ) ICMPv6 protocol. The option is set by default for addresses with prefix length 64. If address is removed or changed, then old prefix<br>will be deprecated by automatically advertising the old prefix with lifetime set to "0s" three times to hosts using ICMPv6 protocol<br>comment  (string;  Descriptive name of an item<br>Default: )<br>disabled  (yes | no Whether address is disabled or not. By default it is not disabled<br>; Default:  no )<br>eui-64  (yes | no;  Whether to calculate EUI-64 address and use it as last 64 bits of the IPv6 address.<br>Default:  no )<br>**----- End of picture text -----**<br>


168 

**==> picture [516 x 129] intentionally omitted <==**

**----- Start of picture text -----**<br>
from-pool  (string;  Name of the pool from which prefix will be taken to construct IPv6 address taking last part of the address from  address  property.<br>Default: )<br>no-dad  (yes | no;  If enabled (yes) - disables Duplicate Address Detection (DAD) for IPv6 addresses on an interface. This can be useful in scenarios<br>Default:  no ) where you want to assign static IPv6 addresses to devices and avoid the delay caused by DAD.<br>interface  (interface Specifies the interface on which the IPv6 address is configured. You can select it from the pool of interfaces available on the router.<br>; Default: )<br>auto-link-local  (ye If newly created address is manual link-local address this setting allows to override dynamically created IPv6 link-local address.<br>s | no; Default:  yes<br>)<br>**----- End of picture text -----**<br>
