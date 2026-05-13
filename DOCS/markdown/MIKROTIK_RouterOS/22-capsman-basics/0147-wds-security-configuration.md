## WDS security configuration 

WDS links can use all available security features. However, they require careful configuration of security parameters. 

It is possible to use one security profile for all clients, and different security profiles for WDS links. Security profile for WDS link is specified in connect-list. Access point always checks connect list before establishing WDS link with another access point, and used security settings from matching connect list entry. WDS link will work when each access point will have connect list entry that matches the other device, has connect =yes and specifies compatible sec urity-profile .
