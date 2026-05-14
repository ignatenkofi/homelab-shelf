## RouterOS Update (1 Firmware Upgrade Image) 

CWMP standard defines that CPE's firmware can be updated using Download RPC with FileType="1 Firmware Upgrade Image" and single URL of a downloadable file (HTTP and HTTPS are supported). Standard also states that downloaded file can be any type and vendor specific process can be applied to finish firmware update. Because MikroTik's update is package based (and also for extra flexibility), an XML file is used to describe firmware upgrade/downgrade. For now, XML configuration supports providing multiple URLs of files, which will be downloaded and applied similarly as regular RouterOS update through firmware/package file upload. 

An example of RouterOS bundle package and tr069-client package update (don't forget to also update tr069-client package). An XML file should be put on some HTTP server, which is accessible from CPE for download. Also, downloadable RouterOS package files should be accessible the same way (can be on any HTTP server). Using ACS execute Download RPC with URL pointing to XML file (e.g. "https://example.com/path/upgrade.xml") with contents: 

248 

```
<upgrade version="1" type="links">
  <config/>
  <links>
      <link>
         <url>https://example.com/routeros-mipsbe-X.Y.Z.npk</url>
      </link>
      <link>
         <url>https://example.com/tr069-client-X.Y.Z-mipsbe.npk</url>
      </link>
  </links>
</upgrade>
```

CPE will download XML, parse/validate its contents, download files from provided URLs and try to upgrade. The result will be reported with TransferComplete RPC. 

**==> picture [13 x 13] intentionally omitted <==**
