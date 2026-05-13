## Introduction 

MikroTik Traffic-Flow is a system that provides statistical information about packets that pass through the router. Besides network monitoring and accounting, system administrators can identify various problems that may occur in the network. With help of Traffic-Flow, it is possible to analyze and optimize the overall network performance. As Traffic-Flow is compatible with Cisco NetFlow, it can be used with various utilities which are designed for Cisco's NetFlow. 

Traffic Flow can process only that traffic which is processed by the router CPU, thus HW offloaded traffic will not be seen in Traffic Flow flows (for example, HW offloaded bridged traffic). 

Traffic-Flow supports the following NetFlow formats: 

- version 1 - This is the original format used by NetFlow. It provides basic information about IP packets flowing through a router but lacks support for advanced features such as different types of protocols and Type of Service (ToS). 

- version 5 - An enhancement over Version 1, this format supports additional features such as Type of Service (ToS), TCP flags, and autonomous system numbers. In addition to version 1, version 5 can include BGP AS and flow sequence number information. Currently, RouterOS does not include BGP AS numbers. 

- version 9 - This version introduces a template-based export format, which allows for extensibility and support for new record types beyond what previous versions could handle. It can export data based on a defined template and is capable of exporting both IPv4 and IPv6 flow information. IPFIX - Standardized by the IETF, this protocol is based on NetFlow Version 9. It expands the capabilities further, allowing for more customizable and flexible flow records. IPFIX supports new technologies that were not addressed by NetFlow, like multicast.
