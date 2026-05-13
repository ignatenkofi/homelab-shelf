## Sub-menu: `/ip/cloud/` 

Back to Home shares the menu with IP Cloud. Back to Home parameters: 

**==> picture [516 x 264] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>back-to-home-vpn (enabled | revoked-and- Enables or revokes and disables the Back to Home service. ddns-enabled has to be set to yes, for BTH to<br>disabled; Default:  revoked-and-disabled ) function.<br>vpn-dns-name (read-only: string) Shows the DNS name assigned to the device. Name consists of product serial number appended by .vpn.<br>mynetname.net. This field is visible only after at least one ddns-request is successfully completed.<br>vpn-port (read-only: integer) Port used by BTH VPN.<br>vpn-status (read-only: string) Contains text string that describes the current BTH state.<br>vpn-relay-rtts  (read-only; "region (ip4: time( Round trip time in milliseconds for each available relay, values are shown both for IPv4 and IPv6.<br>ms ), ip6: time ( ms) ")<br>vpn-relay-ipv4-status  (read-only: string) Status on connection to relay and detailed information about relay<br>vpn-relay-ipv6-status  (read-only: string) Status on connection to relay and detailed information about relay<br>vpn-relay-codes  (read-only: string) Available VPN relay codes, which can be referenced in vpn-prefer-relay-code. All available relays will be<br>shown here.<br>vpn-relay-addressess  (read-only: string) IPv4 address of the relay<br>vpn-relay-addressess-ipv6  (read-only:  IPv6 address of the relay<br>string)<br>**----- End of picture text -----**<br>


876 

**==> picture [516 x 184] intentionally omitted <==**

**----- Start of picture text -----**<br>
vpn-private-key  (read-only: string) Private key for BTH<br>vpn-public-key  (read-only: string) Public key for BTH<br>vpn-peer-private-key  (read-only: string) Peer private key<br>vpn-peer-public-key  (read-only: string) Peer public key<br>vpn-prefer-relay-code  (string;) You can enter relay code that will be preferred for BTH connection, if not set, relay with smallest RTT will<br>be chosen.<br>vpn-interface  (read-only: string) Name of the created interface for Back to Home WireGuard® tunnel.<br>vpn-wireguard-client-config  (read-only:  Configuration that can be entered in your preferred WireGuard® client. Only one client at a time will be<br>string) available to use this config.<br>vpn-wireguard-client-config-qrcode  (read- Scannable QR Code for your preferred WireGuard® client. Only one client at a time will be available to<br>only) use this config.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

When using vpn-wireguard-client-config or vpn-wireguard-client-config-qrcode, both options are equal, you only need to import one of these into your WireGuard client device.
