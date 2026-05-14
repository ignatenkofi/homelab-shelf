## Bridge with NAT 

In this networking setup, all Containers use the same veth interface and communicate with each other without any Firewall restrictions, but you need to forward ports in order to allow access to a Container's port. 

For example, a database Container needs to communicate with a web application Container, the web application needs the port `80` to be exposed to the world, but the database Container does not need any ports to be exposed to the world.
