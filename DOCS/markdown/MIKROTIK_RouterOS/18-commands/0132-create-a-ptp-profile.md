## Create a PTP Profile 

To create a PTP profile, use the following command. In this example, we use the 802.1as profile, but you can select from other available profiles as needed: 

```
/system ptp add name=ptp1 profile=802.1as
```

To verify that the profile has been created successfully, execute: 

```
/system ptp print
```

The output will display the created profile with its current settings: 

```
 Flags: I - inactive, X - disabled
```

```
 0   name="ptp1" priority1=auto priority2=auto delay-mode=auto transport=auto profile=802.1as domain=auto
```

**==> picture [13 x 13] intentionally omitted <==**

By default, parameters for each profile are configured to "auto," which automatically selects the appropriate values based on the profile chosen. Before making manual adjustments, verify that the settings conform to relevant standards (e.g., ITU-T G.8275.1, IEEE 802.1as, SMPTE, AES67). 

1161
