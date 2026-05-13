## Access List 

The access list provides multiple ways of filtering and managing wireless connections. 

RouterOS will check each new connection to see if its parameters match the parameters specified in any access list rule. 

The rules are checked in the order they appear in the list. Only management actions specified in the first matching rule are applied to each connection. 

1336 

Connections, which have been accepted by an access list rule, will be periodically checked, to see if they remain within the permitted time, days and signalrange . If they do not, they will be terminated. 

**==> picture [13 x 13] intentionally omitted <==**

Take care when writing access list rules which reject clients. After being repeatedly rejected by an AP, a client device may start avoiding it. The VLAN ID can't be set by the access list to wifi-qcom-ac interface's clients, without configuring the pvid value for the interface first. 

The access list has two kinds of parameters - filtering, and action. Filtering properties are only used for matching clients, to whom the access list rule should be applied to. Action parameters can change connection parameters for that specific client and potentially overriding its default connection parameters with ones specified in the access list rule.
