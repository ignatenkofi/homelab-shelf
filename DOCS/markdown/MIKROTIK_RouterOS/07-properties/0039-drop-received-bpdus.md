## Drop received BPDUs 

The bridge filter or NAT rules cannot drop BPDUs when the bridge has STP/RSTP/MSTP enabled due to the special processing of BPDUs. However, dropping received BPDUs on a certain port can be done on some switch chips using ACL rules:
