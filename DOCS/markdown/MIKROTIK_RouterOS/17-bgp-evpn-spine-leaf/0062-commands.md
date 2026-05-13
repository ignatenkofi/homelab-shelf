## Commands 

**==> picture [516 x 309] intentionally omitted <==**

**----- Start of picture text -----**<br>
Command Params Description<br>accept accept matched prefix<br>reject reject matched prefix, the prefix will be stored in the memory as "filtered" and will not be the candidate to be selected as the<br>best path.<br>return return to the parent chain<br>jump jump  jump to a specified chain<br>chain_n<br>ame<br>unset unset  used to unset the value of the following properties:<br>prop_na pref-src|bgp-med|bgp-out-med|bgp-local-pref<br>me<br>append append at the end of the list or string. Following property values can be appended:  bgp-communities, bgp-ext-<br>communities, bgp-large-communities, comment<br>filter Inverse of the delete action (Delete everything except the specified values). Values of the following properties can be filtered:<br>bgp-communities, bgp-ext-communities, bgp-large-communities<br>delete Delete the value of the specified property. Values of the following properties can be deleted:  bgp-communities, bgp-<br>ext-communities, bgp-large-communities<br>set set  The command is used to set a new value to writeable properties. Value can be set from other readable properties of<br>prop_wr matching types. For numeric properties, it is possible to prefix the value with +/- which will increment or decrement the<br>iteable current property value by a given amount. For example, " set bgp-local-ref +1 " will increment current LOCAL_PREF<br>value by one, or extract value from other readable num property, " set distance +ospf-ext-metric "<br>**----- End of picture text -----**<br>


1058 

rpki-verify 

_`rpki-`_ Enable RPKI verification in the current chain from the specified RPKI group. _`verify rpki_gr oup_name`_
