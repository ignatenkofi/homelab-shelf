## Multi-WAN setup 

For WireGuard there is no server-client relationship, both ends can serve as an endpoint and both ends are streaming UDP handshake messages to each other if they have endpoints defined in their configurations (this is not always the case, as you can enable "responder" option in the peer settings, which will allow you to emulate server-client behavior, as "server" peer will only reply to the handshake messages from "client" peers and will not stream the handshake messages by itself). 

Because of the described above nature of the tunnel establishment, handshake messages from different endpoints of the WireGuard tunnel are treated as two separate connections. 

We need to take this into account for the setups with multiple path to the "client" peer, as this can cause the "server" to reply to the "client" not via incoming route but via some other route, depending on the setup. 

Further you can see configuration example on how to address this behavior and ensure that "server" uses incoming route to reply back to the "client".
