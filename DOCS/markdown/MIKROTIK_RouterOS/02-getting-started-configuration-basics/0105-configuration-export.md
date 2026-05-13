## Configuration Export 

The following command parameters are accepted: 

**==> picture [516 x 190] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>compact Output only modified configuration, the default behavior<br>file Export configuration to a specified file. When the file is not specified export output will be printed<br>to the terminal<br>show-sensitive (yes|no; Default: no).  RouterOS  Show sensitive information, like passwords, keys, etc.<br>version 7 only<br>Hide sensitive information, like passwords, keys, etc.<br>hide-sensitive  (yes|no; Default: no).  RouterOS<br>version 6 only<br>terse With this parameter, the export command will output only configuration parameters, without<br>defaults.<br>verbose With this parameter, the export command will output whole configuration parameters and items<br>including defaults.<br>**----- End of picture text -----**<br>


For example, export configuration from `/ip address` the menu and save it to a file: 

58 

```
    [admin@MikroTik] > /ip address print
    Flags: X - disabled, I - invalid, D - dynamic
    #   ADDRESS            NETWORK         BROADCAST       INTERFACE
    0   10.1.0.172/24      10.1.0.0        10.1.0.255      bridge1
    1   10.5.1.1/24        10.5.1.0        10.5.1.255      ether1
    [admin@MikroTik] > /ip address export file=address
    [admin@MikroTik] > /file print
    # NAME                            TYPE         SIZE       CREATION-TIME
    0  address.rsc                     script       315        dec/23/2003 13:21:48
    [admin@MikroTik] >
```

By default, the export command writes only user-edited configuration, RouterOS defaults are omitted. 

For example, the IPSec default policy will not be exported, and if we change one property then only our change will be exported: 

```
    [admin@rack1_b4] /ip ipsec policy> print
    Flags: T - template, X - disabled, D - dynamic, I - inactive, * - default
    0 T * group=default src-address=::/0 dst-address=::/0 protocol=all
          proposal=default template=yes
    [admin@rack1_b4] /ip ipsec policy> export
    # apr/02/1970 17:59:14 by RouterOS 6.22
    # software id = DB0D-LK67
    #
    [admin@rack1_b4] /ip ipsec policy> set 0 protocol=gre
    [admin@rack1_b4] /ip ipsec policy> export
    # apr/02/1970 17:59:30 by RouterOS 6.22
    # software id = DB0D-LK67
    #
    /ip ipsec policy
    set 0 protocol=gre
```

**==> picture [13 x 13] intentionally omitted <==**
