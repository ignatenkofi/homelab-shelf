## Configuration example 

This example does not include WireGuard interface configuration as it is applicable to both RoadWarrior and Site ot Site setups with two WAN connections such as for example PCC setup. For these rules to work as intended you need to enable "responder" option in WireGuard peer settings, as "server" could send handshakes via incorrect interface because routing was not marked.
