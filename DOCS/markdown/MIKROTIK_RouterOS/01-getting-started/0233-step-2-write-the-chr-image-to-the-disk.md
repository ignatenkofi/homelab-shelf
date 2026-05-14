## Step 2: Write the CHR image to the disk 

1.  In your web browser, navigate to the MikroTik download page. 2.  Locate the latest Stable RAW CHR disk image. Vultr requires version 7.2.3 Stable or later. 

3.  Right-click the floppy disk icon to copy the URL. Don't download the image now, you'll download it to the server in a later step. 

**==> picture [263 x 189] intentionally omitted <==**

4.  Navigate to the server's information page in the Vultr customer portal. 5.  Connect to the web console. 

**==> picture [246 x 93] intentionally omitted <==**

6.  In the web console, download the CHR image to the server with "wget". If you copied the download URL to your clipboard, you can send it to the server through the web console. 

Substitute your version for x.x.x in the examples that follow. 

```
# wget https://download.mikrotik.com/routeros/x.x.x/chr-x.x.x.img.zip
```

7.  Unzip the downloaded file. 

140 

```
# unzip chr-x.x.x.img.zip
```

8.  Write the MikroTik CHR image to the server's disk with dd. 

```
# dd if=chr-x.x.x.img of=/dev/vda
```

is the image that you unzipped in the previous step. if of is the server's disk:  /dev/vda. 

This procedure takes a couple of minutes; proceed to the next step when complete.
