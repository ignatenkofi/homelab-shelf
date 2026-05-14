## Sub-menu: `/tool graphing queue` 

**==> picture [489 x 136] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>allow-address  (IP/IPv6 prefix; Default: 0.0.0.0/0 ) IP address range from which is allowed to access graphing information<br>allow-target  (yes | no; Default: yes ) Whether to allow access to graphs from queue's target-address<br>comment  (string; Default: ) Description of current entry<br>disabled  (yes | no; Default: no ) Defines whether item is used<br>simple-queue  (all | queue name; Default: all ) Defines which queues will be monitored. all means that all queues on router will be monitored.<br>store-on-disk  (yes | no; Default: yes ) Defines whether to store collected information on system drive.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

If simple queue has target-address set to 0.0.0.0/0 everyone will be able to access queue graphs even if allow address is set to specific address. This happens because by default queue graphs are accessible also from the target address.
