## Multiple user credential export 

It is possible to generate a CSV or XML file with multiple or all user credentials at once by using the export.xml or export.csv as voucher-template. 

```
/user-manager user
```

```
generate-voucher voucher-template=export.xml [find]
```

The command generates an XML file um5files/PRIVATE/GENERATED/vouchers/gen_export.xml which can either be accessible by the WEB browser or any other file access tools. 

342 

```
<?xml version="1.0" encoding="UTF-8"?>
<users>
    <user>
        <username>olsgkl</username>
        <password>86a6zH</password>
    </user>
    <user>
        <username>lkbwss</username>
        <password>jaKY5V</password>
    </user>
    <user>
        <username>cwxbwu</username>
        <password>a62yZd</password>
    </user>
    <user>
        <username>username</username>
        <password>secretpassword</password>
    </user>
</users>
```
