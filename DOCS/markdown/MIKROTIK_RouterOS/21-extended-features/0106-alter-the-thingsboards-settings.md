## Alter the ThingsBoard's settings 

Open " thingsboard.yml " via your preferred text editor (notepad or any other), and alter a few lines. You can backup this file and save it with a different name to have a copy of the default settings, in case, of misconfiguration. 

HTTPS-related settings: 

1.  Enable SSL →  Change "SSL_ENABLED: false " to "SSL_ENABLED: true "; 2.  Change credentials type → from "SSL_CREDENTIALS_TYPE: PEM " to "SSL_CREDENTIALS_TYPE: KEYSTORE "; 3.  Change the path → from "SSL_KEY_STORE: classpath:keystore/keystore.p12 " to "SSL_KEY_STORE: keystore.p12 " (optional); 4.  Disable key alias setting → comment it → just put the " # " symbol in front of the key_alias: "${SSL_KEY_ALIAS:tomcat}" line; 5.  Input your own certificate password that was used in RouterOS → from "SSL_KEY_STORE_PASSWORD: thingsboard " to "SSL_KEY_STORE_PASSWORD: thingsboard_cert_password " and from "SSL_KEY_PASSWORD: thingsboard " to "SSL_KEY_PASSWORD: things board_cert_password ". 

```
  ssl:
    # Enable/disable SSL support
    enabled: "${SSL_ENABLED:true}"
    # Server SSL credentials
    credentials:
      # Server credentials type (PEM - pem certificate file; KEYSTORE - java keystore)
      type: "${SSL_CREDENTIALS_TYPE:KEYSTORE}"
      # Keystore server credentials
      keystore:
        # Type of the key store (JKS or PKCS12)
        type: "${SSL_KEY_STORE_TYPE:PKCS12}"
        # Path to the key store that holds the SSL certificate
        store_file: "${SSL_KEY_STORE:keystore.p12}"
        # Password used to access the key store
        store_password: "${SSL_KEY_STORE_PASSWORD:thingsboard_cert_password}"
        # Key alias
        #key_alias: "${SSL_KEY_ALIAS:tomcat}"
        # Password used to access the key
        key_password: "${SSL_KEY_PASSWORD:thingsboard_cert_password}"
```

MQTT-related settings: 

1.  Enable SSL →  Change "MQTT_SSL_ENABLED: false " to "MQTT_SSL_ENABLED: true "; 2.  Change credentials type → from "MQTT_SSL_CREDENTIALS_TYPE: PEM " to "MQTT_SSL_CREDENTIALS_TYPE: KEYSTORE "; 3.  Change type of key → from "MQTT_SSL_KEY_STORE_TYPE: JKS " to "MQTT_SSL_KEY_STORE_TYPE: PKCS12 "; 4.  Change the path (extension) → from "MQTT_SSL_KEY_STORE:mqttserver .jks " to "MQTT_SSL_KEY_STORE:mqttserver .p12 "; 5.  Disable key alias setting → comment it → just put the " # " symbol in front of the key_alias: "${MQTT_SSL_KEY_ALIAS:}" line; 6.  Input your own certificate password that was used in RouterOS → from "MQTT_SSL_KEY_STORE_PASSWORD: server_ks_password " to "MQTT_SSL_KEY_STORE_PASSWORD: thingsboard_mqttcert_password " and from "MQTT_SSL_KEY_PASSWORD: server_key_password " to "MQTT_SSL_KEY_PASSWORD: thingsboard_mqttcert_password ". 

1892 

```
    ssl:
      # Enable/disable SSL support
      enabled: "${MQTT_SSL_ENABLED:true}"
      # Server SSL credentials
      credentials:
        # Server credentials type (PEM - pem certificate file; KEYSTORE - java keystore)
        type: "${MQTT_SSL_CREDENTIALS_TYPE:KEYSTORE}"
        # Keystore server credentials
        keystore:
          # Type of the key store (JKS or PKCS12)
          type: "${MQTT_SSL_KEY_STORE_TYPE:PKCS12}"
          # Path to the key store that holds the SSL certificate
          store_file: "${MQTT_SSL_KEY_STORE:mqttserver.p12}"
          # Password used to access the key store
          store_password: "${MQTT_SSL_KEY_STORE_PASSWORD:thingsboard_mqttcert_password}"
          # Optional alias of the private key; If not set, the platform will load the first private key from
the keystore;
          #key_alias: "${MQTT_SSL_KEY_ALIAS:}"
          # Optional password to access the private key. If not set, the platform will attempt to load the
private keys that are not protected with the password;
          key_password: "${MQTT_SSL_KEY_PASSWORD:thingsboard_mqttcert_password}"
```

**==> picture [13 x 12] intentionally omitted <==**

Leave the rest of the settings at default values. Do not delete/change lines that are not shown in the examples above unless you know what you are doing. 

Apply the changes to the " thingsboard.yml " file (re-save it after editing).
