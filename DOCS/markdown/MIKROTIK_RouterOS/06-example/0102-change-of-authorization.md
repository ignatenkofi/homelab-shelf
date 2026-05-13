## Change of Authorization 

RADIUS disconnect and Change of Authorization (according to RFC3576) are supported as well. These attributes may be changed by a CoA request from the RADIUS server: 

- Mikrotik-Group Mikrotik-Recv-Limit Mikrotik-Xmit-Limit Mikrotik-Rate-Limit Ascend-Data-Rate (only if Mikrotik-Rate-Limit is not present) Ascend-XMit-Rate (only if Mikrotik-Rate-Limit is not present) Mikrotik-Mark-Id Filter-Id Mikrotik-Advertise-Url Mikrotik-Advertise-Interval Session-Timeout Idle-Timeout Port-Limit 

Note that it is not possible to change IP address, pool or routes that way - for such changes a user must be disconnected first.
