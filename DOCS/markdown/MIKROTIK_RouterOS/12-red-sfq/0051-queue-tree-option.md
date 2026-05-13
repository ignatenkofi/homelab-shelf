## Queue Tree option 

Mark all packets with packet-marks upload/download: (let's consider that ether1-WAN is the public interface to the Internet and ether2-LAN is a local interface where clients are connected): 

723 

```
/ip firewall mangle add chain=prerouting action=mark-packet \
   in-interface=ether2-LAN new-packet-mark=client_upload
/ip firewall mangle add chain=prerouting action=mark-packet \
   in-interface=ether1-WAN new-packet-mark=client_download
```

Then, two queue rules are required, one for download and one for upload: 

```
/queue tree add parent=global queue=PCQ_download packet-mark=client_download
/queue tree add parent=global queue=PCQ_upload packet-mark=client_upload
```
