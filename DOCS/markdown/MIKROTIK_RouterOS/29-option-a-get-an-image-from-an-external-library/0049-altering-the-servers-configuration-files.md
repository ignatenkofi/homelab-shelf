## Altering the server's configuration files 

To access the server's configuration files ( clients.conf and authorize ), we will need to use SFTP (file transfer over SSH) protocol, so make sure that SSH se rvice is enabled. 

Open your command terminal ("CMD", as Administrator, for Windows users, or "Linux Shell or Command Terminal" for Linux users) and navigate it to the directory where you want to download the configuration files. For example, to "radius" folder on your "Desktop": 

```
C:\WINDOWS\system32>cd C:\Users\Administrator\Desktop\radius
```

```
C:\Users\Administrator\Desktop\radius>
```

Initiate SFTP to the device's IP address: 

1861 

```
C:\Users\DenissPC\Desktop\radius>sftp admin@10.55.8.53
admin@10.55.8.53's password:
Connected to 10.55.8.53.
sftp>
```

Go to the server's configuration file folder (use `dir` or `ls` command to see the content of the folder you are in and `cd` command to go to the folder of our choice). 

The first file, "clients.conf" allows you to define RADIUS clients. Per the "freeradius" documentation, it should be under the "/etc/freeradius" directory...so, navigate there and use `get` command to download it: 

```
sftp> dir
freeradius          pub                     pull                    skins
sftp> cd freeradius/etc/freeradius
sftp> dir
README.rst          certs               clients.conf        dictionary          experimental.conf
hints
huntgroups          mods-available      mods-config         mods-enabled        panic.gdb           policy.
d
proxy.conf          radiusd.conf        sites-available     sites-enabled       templates.conf      trigger.
conf
users
sftp> get clients.conf
Fetching /freeradius/etc/freeradius/clients.conf to clients.conf
/freeradius/etc/freeradius/clients.conf                                               100% 8323     1.2MB/s
00:00
```

Open " clients.conf " via your preferred text editor (notepad or any other). You can study the file to see all the options that you have (additionally, check freer adius.org). This example shows a basic setup, so, we will just overwrite the whole file with the lines shown below: 

```
client new {
    ipaddr = 0.0.0.0/0
    secret = client_password
}
```

where we indicate, that our radius client can connect using any possible IP address ( ipaddr=0.0.0.0/0 ensures that, but you also can change it to the actual ip address/mask of your radius client if you require to do so) and that our secret is "client_password" (you can change it to any other secret). 

Save the file/overwrite it. 

The second file, "authorize" allows you to set up users. Per the "freeradius" documentation, it should be under "/etc/freeradius/mods-config/files". Go there and `get` the file: 

```
sftp> dir
freeradius          pub                     pull                    skins
sftp> cd freeradius/etc/freeradius/mods-config/files
sftp> dir
accounting  authorize   dhcp        pre-proxy
sftp> get authorize
Fetching /freeradius/etc/freeradius/mods-config/files/authorize to authorize
/freeradius/etc/freeradius/mods-config/files/authorize                                100% 6594     1.1MB/s
00:00
```

Open " authorize " via your preferred text editor (notepad or any other). This example shows a basic setup, so, we will just uncomment (remove the "#" symbol from) the line shown below (leave the rest of the configuration/lines as they are): 

```
bob        Cleartext-Password := "hello"
```

1862 

which creates a username "bob" and sets the password to "hello" (you can change the username and password). 

Save the file/overwrite it. 

Upload both files back/overwrite the default files with the help of the `put` command: 

```
sftp> dir
freeradius          pub                     pull                    skins
sftp> cd freeradius/etc/freeradius
sftp> dir
README.rst          certs               clients.conf        dictionary          experimental.conf
hints
huntgroups          mods-available      mods-config         mods-enabled        panic.gdb           policy.
d
proxy.conf          radiusd.conf        sites-available     sites-enabled       templates.conf      trigger.
conf
users
sftp> put clients.conf
Uploading clients.conf to /freeradius/etc/freeradius/clients.conf
clients.conf                                                                          100%   67    22.3KB/s
00:00
sftp> cd mods-config/files
sftp> dir
accounting  authorize   dhcp        pre-proxy
sftp> put authorize
Uploading authorize to /freeradius/etc/freeradius/mods-config/files/authorize
authorize                                                                             100% 6626     1.6MB/s
00:00
```

Restart the container: 

```
/container/stop 0
/container/start 0
```

Make sure to wait for the container to stop ( `status=stopped` should be shown after using `/container/print` command) before initiating it again.
