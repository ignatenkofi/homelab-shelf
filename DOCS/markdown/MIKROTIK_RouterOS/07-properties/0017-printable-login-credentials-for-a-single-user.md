## Printable login credentials for a single user 

To generate a single user's printable voucher card, simply use the generate-voucher command. Specify the RouterOS ID number of the user or use the find command to specify a username. A template is already included in User Manager's installation available in the Files section of your device. You can customize the template for your needs. 

```
/user-manager user
```

```
generate-voucher voucher-template=printable_vouchers.html [find where name=username]
```

The generated voucher card is available by accessing the router using a WEB browser and navigating to /um/PRIVATE/GENERATED/vouchers /gen_printable_vouchers.html 

By default, the printable card looks like this: 

**==> picture [338 x 189] intentionally omitted <==**

**==> picture [13 x 13] intentionally omitted <==**

To access the PRIVATE path of the /um/ directory by the WEB browser, private-username and private-password must be configured. See Settin gs section. 

It is possible to use different variables when generating vouchers. Currently, supported variables are: 

$(username) - Represents User Manager username 

$(password) - Password of the username 

$(userprofname) - Profile that is active for the particular user 

$(userprofendtime) - Profile validity end time if specified
