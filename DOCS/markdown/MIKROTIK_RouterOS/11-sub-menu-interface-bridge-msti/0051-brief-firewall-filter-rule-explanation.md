## Brief firewall filter rule explanation: 

- packets with connection-state=established,related added to FastTrack for faster data throughput, the firewall will work with new connections only; drop invalid connection and log them with prefix "invalid"; drop attempts to reach not public addresses from your local network, apply address-list=not_in_internet before, "bridge" is local network interface, log=yes attempts with prefix "!public_from_LAN"; 

- drop incoming packets that are not NAT`ed, ether1 is public interface, log attempts with "!NAT" prefix; jump to ICMP chain to drop unwanted ICMP messages 

- drop incoming packets from the Internet, which are not public IP addresses, ether1 is a public interface, log attempts with prefix "!public"; drop packets from LAN that does not have LAN IP, 192.168.88.0/24 is local network used subnet;
