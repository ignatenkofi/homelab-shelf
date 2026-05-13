## WDS and WPA/WPA2 

1419 

If access point uses security profile with mode =dynamic-keys, then encryption will be used for all WDS links. Since WPA authentication and key exchange is not symmetrical, one of the access points will act as a client for the purpose of establishing secure connection. This is similar to how static-mesh and dyn amic-mesh WDS modes work. Some problems, like single sided WDS link between two incorrectly configured access points that use non-mesh mode, is not possible if WPA encryption is enabled. However, non-mesh modes with WPA still have other issues (like constant reconnection attempts in case of configuration mismatch) that are solved by use of the -mesh WDS modes. 

In general, WPA properties on both access points that establish WPA protected WDS link have to match. These properties are authentication-types , unicast -ciphers , group-ciphers . For non-mesh WDS mode these properties need to have the same values on both devices. In mesh WDS mode each access point has to support the other one as a client. 

Theoretically it is possible to use RADIUS MAC authentication and other RADIUS services with WDS links. However, only one access point will interact with the RADIUS server, the other access point will behave as a client. 

Implementation of eap-tls EAP method in RouterOS is particularly well suited for WDS link encryption. tls-mode =no-certificates requires no additional configuration, and provides very strong encryption.
