## Removing and disabling connections 

In the smartphone app, the VPN configuration is added to the System VPN settings. In this regard, the Back to Home app only acts as a wizard. It supplies needed config to the operating system (this is why iPhone will warn you about altering system configuration). 

To remove the created connection, go into the smartphone settings app and remove the VPN connections from there. 

In the MikroTik router side, you should manually delete the added Peers in the Wireguard menu. Note that "revoke-and-disable" button can't be used to "Pause" the use of the Back to Home feature. Once you revoke-and-disable in RouterOS, all Peers will be disassociated from the Cloud / Relay servers, and you will have to re-create the connection from the Smartphone app. Therefore, once you have used the option "revoke-and-disable" in RouterOS IP Cloud menu, you need to also delete the Peers from the Wireguard menu, as they can't be re-used.
