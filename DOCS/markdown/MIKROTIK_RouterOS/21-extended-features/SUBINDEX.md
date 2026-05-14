# Extended features

Chapter 21. PDF pages 1844–1907. 130 sections.

[← back to top index](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/INDEX.md)

## Extended features

*3 sections*

- [Container](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0001-container.md)
- [Disclaimer](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0002-disclaimer.md)
- [Security risks:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0003-security-risks.md)

## Container

*112 sections*

- [Container configuration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0004-container-configuration.md)
- [Running Pi-hole](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0005-running-pi-hole.md)
- [Steps to run Pi-hole](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0006-steps-to-run-pi-hole.md)
- [2.  Create a new veth interface and assign an IP address in a range that is unique in your network:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0007-2-create-a-new-veth-interface-and-assign-an-ip-address-in-a-range-that.md)
- [3.  Create a new bridge that is going to be used for your Containers and assign the same IP address that was used for the veth interface's gateway:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0008-3-create-a-new-bridge-that-is-going-to-be-used-for-your-containers-and.md)
- [4.  Add the veth interface to your newly created bridge:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0009-4-add-the-veth-interface-to-your-newly-created-bridge.md)
- [5.  Create a NAT for outgoing traffic:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0010-5-create-a-nat-for-outgoing-traffic.md)
- [6.  Create environment variables for the Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0011-6-create-environment-variables-for-the-container.md)
- [7.  Create mounted volumes for the Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0012-7-create-mounted-volumes-for-the-container.md)
- [9.  Add a Containter:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0013-9-add-a-containter.md)
- [11.  Start the Containter:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0014-11-start-the-containter.md)
- [Adding a Container image](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0015-adding-a-container-image.md)
- [Option A: Get an image from an external library](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0016-option-a-get-an-image-from-an-external-library.md)
- [Option B: Import image from PC](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0017-option-b-import-image-from-pc.md)
- [Option C: Build an image on PC](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0018-option-c-build-an-image-on-pc.md)
- [4.  Upload the archive to your RouterOS device, for example:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0019-4-upload-the-archive-to-your-routeros-device-for-example.md)
- [Alternative: Using Docker to build Container images](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0020-alternative-using-docker-to-build-container-images.md)
- [should return:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0021-should-return.md)
- [If not - install extra architectures:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0022-if-not---install-extra-architectures.md)
- [Upload pihole.tar to Your RouterOS device.](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0023-upload-piholetar-to-your-routeros-device.md)
- [Create a container from the tar image](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0024-create-a-container-from-the-tar-image.md)
- [Networking examples](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0025-networking-examples.md)
- [Bridge with NAT](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0026-bridge-with-nat.md)
- [The network configuration:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0027-the-network-configuration.md)
- [The database Container configuration:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0028-the-database-container-configuration.md)
- [The webapp Container configuration:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0029-the-webapp-container-configuration.md)
- [Isolated Containers](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0030-isolated-containers.md)
- [Container in Layer2 network](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0031-container-in-layer2-network.md)
- [IPv4 and IPv6 for Container](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0032-ipv4-and-ipv6-for-container.md)
- [Tips and tricks](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0033-tips-and-tricks.md)
- [Containerized App management](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0034-containerized-app-management.md)
- [Security Considerations](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0035-security-considerations.md)
- [Setup Wizard](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0036-setup-wizard.md)
- [Step 1: Storage Selection](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0037-step-1-storage-selection.md)
- [Step 2: Bridge Configuration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0038-step-2-bridge-configuration.md)
- [Step 3: IP Configuration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0039-step-3-ip-configuration.md)
- [Completion](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0040-completion.md)
- [Storage Configuration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0041-storage-configuration.md)
- [Network Configuration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0042-network-configuration.md)
- [Registry and Updates](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0043-registry-and-updates.md)
- [Storage Paths](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0044-storage-paths.md)
- [User Interface](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0045-user-interface.md)
- [Application Management](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0046-application-management.md)
- [Status Indicators and Metadata](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0047-status-indicators-and-metadata.md)
- [Application Lifecycle Management](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0048-application-lifecycle-management.md)
- [Cleanup Command](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0049-cleanup-command.md)
- [Available Applications by Category](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0050-available-applications-by-category.md)
- [Container - freeradius server](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0051-container---freeradius-server.md)
- [Setup NAT for outgoing traffic if required:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0052-setup-nat-for-outgoing-traffic-if-required.md)
- [Getting image](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0053-getting-image.md)
- [Altering the server's configuration files](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0054-altering-the-servers-configuration-files.md)
- [Result verification](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0055-result-verification.md)
- [Container - HAProxy](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0056-container---haproxy.md)
- [Advanced: HAProxy with Certbot](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0057-advanced-haproxy-with-certbot.md)
- [3.  Create the Certbot Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0058-3-create-the-certbot-container.md)
- [6.  Start HAProxy Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0059-6-start-haproxy-container.md)
- [8.  Done](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0060-8-done.md)
- [Container - HomeAssistant](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0061-container---homeassistant.md)
- [Environment variables and mounts](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0062-environment-variables-and-mounts.md)
- [Home-Assistant setup](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0063-home-assistant-setup.md)
- [Resources](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0064-resources.md)
- [Container - Matrix](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0065-container---matrix.md)
- [1.  Create PostgreSQL Container environment variables:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0066-1-create-postgresql-container-environment-variables.md)
- [3.  Create a PostgreSQL Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0067-3-create-a-postgresql-container.md)
- [4.  Create Synapse Container environment variables:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0068-4-create-synapse-container-environment-variables.md)
- [5.  Create Synapse Container mounts:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0069-5-create-synapse-container-mounts.md)
- [Discord bridge](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0070-discord-bridge.md)
- [2.  Create PostgreSQL Discord bridge Container mounts:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0071-2-create-postgresql-discord-bridge-container-mounts.md)
- [3.  Create a PostgreSQL Container for Discord bridge:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0072-3-create-a-postgresql-container-for-discord-bridge.md)
- [6.  Create a Discord Bridge Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0073-6-create-a-discord-bridge-container.md)
- [7.  Start and stop the Discord bridge Container to generate files:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0074-7-start-and-stop-the-discord-bridge-container-to-generate-files.md)
- [Container - mosquitto MQTT server](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0075-container---mosquitto-mqtt-server.md)
- [Container mode](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0076-container-mode.md)
- [Networking](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0077-networking.md)
- [Pull image:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0078-pull-image.md)
- [Setting up mosquitto configuration file](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0079-setting-up-mosquitto-configuration-file.md)
- [Initiate SFTP to the device's IP address:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0080-initiate-sftp-to-the-devices-ip-address.md)
- [Restart the container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0081-restart-the-container.md)
- [Starting the container](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0082-starting-the-container.md)
- [MQTT publish and subscribe](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0083-mqtt-publish-and-subscribe.md)
- [Add an MQTT broker:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0084-add-an-mqtt-broker.md)
- [Subscribe to the MQTT broker and the required topic:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0085-subscribe-to-the-mqtt-broker-and-the-required-topic.md)
- [SSL MQTT](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0086-ssl-mqtt.md)
- [To increase security, use SSL MQTT.](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0087-to-increase-security-use-ssl-mqtt.md)
- [Server configuration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0088-server-configuration.md)
- [Confirm that the broker listens on port 8883 using the logs:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0089-confirm-that-the-broker-listens-on-port-8883-using-the-logs.md)
- [Testing the connection](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0090-testing-the-connection.md)
- [Add MQTT broker for SSL connection:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0091-add-mqtt-broker-for-ssl-connection.md)
- [Publish a static MQTT message:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0092-publish-a-static-mqtt-message.md)
- [Container - Postgres](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0093-container---postgres.md)
- [Advanced: Postgres with Pgadmin](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0094-advanced-postgres-with-pgadmin.md)
- [3.  Create the Pgadmin Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0095-3-create-the-pgadmin-container.md)
- [4.  Disable Webfig:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0096-4-disable-webfig.md)
- [5.  Start Pgadmin Container:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0097-5-start-pgadmin-container.md)
- [Container - ThingsBoard MQTT/HTTP server](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0098-container---thingsboard-mqtthttp-server.md)
- [Setup NAT for outgoing traffic:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0099-setup-nat-for-outgoing-traffic.md)
- [Mounts:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0100-mounts.md)
- [Management access](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0101-management-access.md)
- [MQTT test](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0102-mqtt-test.md)
- [Enabling HTTPS and SSL MQTT](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0103-enabling-https-and-ssl-mqtt.md)
- [Create certificates](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0104-create-certificates.md)
- [Download the ThingsBoard's configuration file](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0105-download-the-thingsboards-configuration-file.md)
- [Alter the ThingsBoard's settings](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0106-alter-the-thingsboards-settings.md)
- [Upload altered ThingsBoard configuration file](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0107-upload-altered-thingsboard-configuration-file.md)
- [Confirm HTTPS access](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0108-confirm-https-access.md)
- [Confirm SSL MQTT connection](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0109-confirm-ssl-mqtt-connection.md)
- [Testing with the device that is running the container](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0110-testing-with-the-device-that-is-running-the-container.md)
- [Add MQTT broker:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0111-add-mqtt-broker.md)
- [Publish a static test MQTT message in the JSON format:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0112-publish-a-static-test-mqtt-message-in-the-json-format.md)
- [Testing with another device](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0113-testing-with-another-device.md)
- [Import the certificate:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0114-import-the-certificate.md)
- [DLNA Media server](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0115-dlna-media-server.md)

## DLNA Media server

*3 sections*

- [Server settings](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0116-server-settings.md)
- [Share settings](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0117-share-settings.md)
- [Sub-menu: `/ip smb shares`](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0118-sub-menu-ip-smb-shares.md)

## SMB

*8 sections*

- [User setup](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0119-user-setup.md)
- [Sub-menu: `/ip smb user`](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0120-sub-menu-ip-smb-user.md)
- [add shared folder:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0121-add-shared-folder.md)
- [enable SMB service:](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0122-enable-smb-service.md)
- [UPS](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0123-ups.md)
- [Sub-menu: `/system ups`](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0124-sub-menu-system-ups.md)
- [Connecting the UPS unit](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0125-connecting-the-ups-unit.md)
- [General Properties](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0126-general-properties.md)

## UPS

*2 sections*

- [Runtime Calibration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0127-runtime-calibration.md)
- [Wake on LAN](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0128-wake-on-lan.md)

## Wake on LAN

*2 sections*

- [IP packing](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0129-ip-packing.md)
- [Packing configuration](https://raw.githubusercontent.com/ignatenkofi/gh.project.homelab/main/DOCS/markdown/MIKROTIK_RouterOS/21-extended-features/0130-packing-configuration.md)
