## General properties 

```
/ip upnp
```

**==> picture [511 x 165] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>allow-disable- whether or not the users are allowed to disable the router's external interface. This functionality (for users to be able to turn the<br>external- router's external interface off without any authentication procedure) is required by the standard, but as it is sometimes not expected<br>interface  (yes  or unwanted in UPnP deployments which the standard was not designed for (it was designed mostly for home users to establish their<br>| no ; Default: y own local networks), you can disable this behavior<br>es )<br>enabled  (yes |  Enable UPnP service<br>no ; Default: no<br>)<br>show-dummy- Enable a workaround for some broken implementations, which are handling the absence of UPnP rules incorrectly (for example,<br>rule  (yes | no ;  popping up error messages). This option will instruct the server to install a dummy (meaningless) UPnP rule that can be observed by<br>Default: yes ) the clients, which refuse to work correctly otherwise<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

If you do not disable the allow-disable-external-interface , any user from the local network will be able (without any authentication procedures) to disable the router's external interface
