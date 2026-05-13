## 60-day trial 

In addition to the limited Free installation, you can also test the increased speed of P1/P10/PU licenses with a 60 trial. 

You will have to have an account registered on MikroTik.com. Then you can request the desired license level for trial from your router that will assign your router ID to your account and enable the purchase of the license from your account. All the paid license equivalents are available for trial. A trial period is 60 days from the day of acquisition after this time passes, your license menu will start to show "Limited upgrades", which means that RouterOS can no longer be upgraded or change packages (disabling or enabling packages). 

If you plan to purchase the selected license, you should do it within 60 days of the trial end date. If your trial ends, and there are no purchases within 2 months after it ended, the device will no longer appear in your MikroTik account. You will have to make a new CHR installation to make a purchase within the required time frame. 

To request a trial license, you must run the command " /system license renew " from the CHR device command line. You will be asked for the username and password of your mikrotik.com account. 

**==> picture [13 x 13] intentionally omitted <==**

If you plan to use multiple virtual systems of the same kind, it may be possible that the next machine has the same system ID as the original one. This can happen on certain cloud providers, such as Linode. To avoid this, after your first boot, run the command "/system license generate-new-id" before you request a trial license. Note that this feature must be used only while CHR is running on a free type of RouterOS license. If you have already obtained a paid or trial license, do not use the regenerate feature since you will not be able to update your current key anymore 

**==> picture [13 x 13] intentionally omitted <==**

IP/Cloud requires a paid perpetual license for Cloud Hosted Router (CHR). 

An expired CHR license means the CHR instance failed to renew its license before the "deadline-at" date by contacting the MikroTik server or that the 60day trial period has ended. While the router continues operating at the same tier, software updates and package changes are disabled. 

It is only possible to license an expired CHR instance using a Prepaid key.
