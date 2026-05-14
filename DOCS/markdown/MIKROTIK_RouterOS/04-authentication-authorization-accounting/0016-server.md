## Server 

A RouterOS dot1x server acts as an authenticator. An interface where dot1x server is enabled will block all traffic except for EAPOL packets which is used for the authentication. After client is successfully authenticated, the interface will accept all received traffic on the port. If the interface is connected to a shared medium with multiple hosts, the traffic will be accepted from all hosts when at least one client is successfully authenticated. However, it is possible to configure dynamic switch rules to accept only the authenticated user source MAC address and drop all other source MAC addresses. In case of failed authentication, it is possible to accept the traffic with a dedicated port VLAN ID. 

**==> picture [13 x 13] intentionally omitted <==**

When a dot1x server is created on a bridge port, the bridge should be running (R/M)STP, otherwise EAP packets from the client will not be correctly accepted. Bridge interface is created with `protocol-mode=rstp` by default. If the bridge port should not send any BPDUs or any received BPDUs should be ignored, use `edge=yes` configuration on bridge ports.
