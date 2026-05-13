## Overview 

Simple Network Management Protocol (SNMP) is an Internet-standard protocol for managing devices on IP networks. SNMP can be used to graph various data with tools such as CACTI, MRTG, or The Dude. 

SNMP write support is only available for some OIDs. For supported OIDs SNMP v1, v2 or v3 write is supported. 

**==> picture [453 x 165] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

SNMP will respond to the query on the interface SNMP request was received from forcing responses to have same source address as request destination sent to the router 

**==> picture [13 x 13] intentionally omitted <==**

SNMP tool collects data from different services running on the system. If, for some reason, communication between SNMP and some service is taking longer time than expected (30 seconds per service, 5 minutes for routing service), you will see a warning in the log stating "timeout while waiting for program" or "SNMP did not get OID data within expected time, ignoring OID". After that, this service will deny SNMP requests for a while before even trying to get requested data again. 

This error has nothing to do with SNMP service itself. In most cases, such an error is printed when some slow or busy service is monitored through SNMP, and quite often, it is a service that should not be monitored through SNMP, and proper solution in such cases is to skip such OIDs on your monitoring tool.
