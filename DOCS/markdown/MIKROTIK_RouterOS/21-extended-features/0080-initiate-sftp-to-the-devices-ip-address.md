## Initiate SFTP to the device's IP address: 

```
C:\Users\Administrator\Desktop\Container>sftp admin@192.168.88.1
The authenticity of host '192.168.88.1 (192.168.88.1)' can't be established.
RSA key fingerprint is SHA256:lfxxs+xMrXlvP7hiHi9ZAEZlPi6/c5US+r6J7ljhkaA.
Are you sure you want to continue connecting (yes/no/[fingerprint])?yes
Warning: Permanently added '192.168.88.1' (RSA) to the list of known hosts.
Connected to 192.168.88.1.
sftp>
```

Go to the mosquitto configuration file folder (use `dir` or `ls` command to see the content of the folder you are in and `cd` command to go to the folder of our choice). By default, the configuration is loaded from the "/mosquitto/config/mosquitto.conf", so, navigate there and use `get` command to download it: 

```
sftp> cd mosquitto/mosquitto/config
sftp> dir
mosquitto.conf
sftp> get mosquitto.conf
Fetching /mosquitto/mosquitto/config/mosquitto.conf to mosquitto.conf
/mosquitto/mosquitto/config/mosquitto.conf
```

Open " mosquitto.conf " via your preferred text editor (notepad or any other), and just overwrite it with two lines shown below: 

**==> picture [13 x 13] intentionally omitted <==**

In this section, we will configure a basic non-SSL MQTT setup for testing purposes. Non-SSL MQTT is not secure for a production environment unless you are certain the required security/restrictions are in place. 

For a production environment, topologies where the MQTT traffic can be captured/sniffed and/or topologies where the MQTT traffic is routed directly via the internet (not locally), use SSL MQTT. Check the SSL MQTT section for more information. 

```
listener 1883
allow_anonymous true
```

The first line, listener 1883 , will make the installation listen for incoming network connection on the specified port. The second line, allow_anonymous true , determines whether clients that connect without providing a username are allowed to connect. 

Overwrite the file using the same mosquitto.conf name. 

After you have created your own custom configuration file, upload it into the mounted directory/folder " mosquitto_mounted ". If you have not run the container yet, you will not have the " mosquitto_mounted " folder and you can create it manually. If you did run it ( `/container start 0` ), it should have been created automatically: 

```
sftp> dir
```

```
mosquitto           mosquitto_mounted   pub                 pull                skins
```

Use SFTP from the directory where the edited mosquitto.conf file is located and `put` it into the mounted directory: 

1877 

```
C:\Users\Administrator\Desktop\Container>dir
 Directory of C:\Users\Administrator\Desktop\Container
```

```
02/03/2023  12:09 PM    <DIR>          .
02/03/2023  12:09 PM    <DIR>          ..
02/03/2023  12:09 PM            40,449 mosquitto.conf
               1 File(s)         40,449 bytes
               2 Dir(s)  76,166,430,720 bytes free
```

```
C:\Users\Administrator\Desktop\Container>sftp admin@192.168.88.1
Connected to 192.168.88.1.
sftp> dir
mosquitto           mosquitto_mounted   pub                 pull                skins
sftp> cd mosquitto_mounted
sftp> put mosquitto.conf
Uploading mosquitto.conf to /mosquitto_mounted/mosquitto.conf
mosquitto.conf                                                                        100%  162    40.5KB/s
00:00
```
