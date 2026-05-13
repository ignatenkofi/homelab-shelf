## Port knocking 

All available public IP addresses are constantly being port scanned by bots and services like shodan.io and anyone can use this information to perform brute-force attacks and execute any known exploits. Port knocking is a cost-effective way to defend against this by not exposing any ports and simply listening to connection attempts - if the correct sequence of port connection attempts is made, the client is considered safe and added to a list of secured address list that bypass the WAN firewall rules.
