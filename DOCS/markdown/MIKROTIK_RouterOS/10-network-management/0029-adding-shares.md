## Adding shares 

First, attach your USB drive and determine the file path of the directory you want to share: 

```
[user@RouterOS] > file/print
 # NAME                                                                           TYPE             SIZE LAST-
MODIFIED
 0 web                                                                            directory             2025-01-
23 09:29:42
 1 usb1                                                                           disk                  2025-01-
22 09:45:57
 2 pub                                                                            directory             2025-01-
23 09:24:41
 3 skins                                                                          directory             2024-12-
10 08:19:27
 4 pub/index.html                                                                 .html file        670 2025-01-
23 09:24:41
 5 skins/default.json                                                             .json file        151 2024-07-
15 10:20:11
 6 usb1/Secret Files                                                                  directory
2024-03-18 09:01:41
 7 usb1/forum                                                                     directory             2025-01-
22 10:58:20
 8 usb1/Secret Files/Home Video.srt                                                                           .
srt file         267 2020-06-01 11:29:14
 9 usb1/Secret Files/Home Video.mp4                                                                           .
mp4 file   1584.4MiB 2020-06-01 11:34:33
10 usb1/forum/cat.jpeg                                                            .jpeg file  4307.7KiB 2025-01-
22 09:38:55
11 usb1/forum/cat1.jpeg                                                           .jpeg file   231.8KiB 2025-01-
22 10:58:20
12 usb1/forum/cat2.jpeg                                                           .jpeg file   129.6KiB 2025-01-
22 10:58:20
13 usb1/forum/cat3.jpeg                                                           .jpeg file   263.8KiB 2025-01-
22 10:58:20
14 usb1/forum/cat4.jpeg                                                           .jpeg file   438.4KiB 2025-01-
22 10:58:20
15 web/index.html                                                                 .html file       1473 2025-01-
23 09:29:42
```

Now in the ip/cloud menu go to file share, and add a new share, specifying the expiration date and whether the other user will have permission to upload files to your router: 

```
[user@RouterOS] /ip/cloud/back-to-home-file> add allow-uploads=no expires=never path="usb1/Secret Files/"
```

Now you can issue the print command to see if the share link has been made and what the URL is to copy for sharing: 

878 

```
[user@RouterOS] /ip/cloud/back-to-home-file> print
Columns: PATH, URL, DIRECT-URL, EXPIRES, DOWNLOADS
```

```
# PATH                      URL                                                        DIRECT-
URL                                                    EXPIRES  DOWNLOADS
```

```
0 /usb1/Secret Files  https://acf017skgys.routingthecloud.net/s/4MPgHbEZCZYGVtp  https://acf017skgys.
routingthecloud.net/s/4MPgHbEZCZYGVtp?dl  never            5
```

```
1 /usb1/Secrets      https://acf017skgys.routingthecloud.net/s/K8zkh1UjKuqtEQ0  https://acf017skgys.
routingthecloud.net/s/K8zkh1UjKuqtEQ0?dl  never            2
```

```
[user@RouterOS] /ip/cloud/back-to-home-file>
```

Now, if you copy the "URL", you can share it with other people, regardless of where they are located, and regardless of whether your router has a public IP or not. 

When you send the URL to a friend, they can then see all the files in the shared directory and can download them. If you enabled uploads in the share creation process, they can also upload files into your router. Keep this URL safe, or specify "expires" date to avoid other people accessing these files. 

**==> picture [505 x 288] intentionally omitted <==**

**==> picture [516 x 179] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>enable  (Default) Enables the File Share function. The File Share service will be activated when the first share is added. If no shares are<br>present, the File Share service remains disabled.<br>disabled  (yes | no; Default: Disables the File share function.<br>no )<br>allow-uploads  (yes | no; D Enables the option for anyone to upload files to your router.<br>efault:  no )<br>expires  (Default:  never ) Share expires date. Format: ISO 8601 (2025-01-25 00:00:00)<br>Example: /ip/cloud/back-to-home-file set 0 expires="2025-01-25 07:15:00"<br>path Sets the path for the file to be shared.<br>Example: "/ip/cloud/back-to-home-file/add path=mypath/myfile"<br>**----- End of picture text -----**<br>

WinBox GUI 

879 

To share the file, access the "File Shares" menu located under the IP → Cloud "Configuration" section. 

**==> picture [505 x 316] intentionally omitted <==**

To create a new share, set the "Path", "Expires" and "Auto uploads" options. 

880 

**==> picture [505 x 350] intentionally omitted <==**

```
[admin@MikroTik] > ip/cloud/back-to-home-file/print detail
Flags: X - disabled; I - invalid
```

```
 0    path=/mypath/myfile allow-uploads=no expires=2025-01-25 07:15:00 key="*********"
      url="https://*********.routingthecloud.net/s/*********" direct-url="https://*********.routingthecloud.net
/s/*********"
```

```
      downloads=0
```

**==> picture [13 x 13] intentionally omitted <==**
