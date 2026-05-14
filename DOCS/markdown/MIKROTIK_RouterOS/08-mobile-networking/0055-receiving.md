## Receiving 

RouterOS also supports receiving of SMS messages, can execute scripts, and even respond to the sender. 

Before the router can receive SMS, the relevant configuration is required in the `/tool sms` menu. The following parameters are configurable: 

**==> picture [516 x 82] intentionally omitted <==**

**----- Start of picture text -----**<br>
Parameter Description<br>allowed-number  (st The sender number that will be allowed to run commands, must specify the country code ie. +371XXXXXXX<br>ring; Default: "")<br>channel  (integer;  Which modem channel to use for receiving.<br>Default: ) 0<br>**----- End of picture text -----**<br>

828 

**==> picture [516 x 178] intentionally omitted <==**

**----- Start of picture text -----**<br>
keep-max-sms  (int Maximum number of messages that will be saved. If you set this bigger than SIM supports, new messages will not be received.<br>eger; Default: ) 0 Replaced with  auto-erase  parameter starting from RouterOS v6.44.6<br>auto-erase  (yes |  SIM storage size is read automatically. When  auto-erase=no  new SMS will not be received if storage is full. Set  auto-<br>no; Default:  no ) erase=yes  to delete the oldest received SMS to free space for new ones automatically. Available starting from v6.44.6<br>port  (string;  Modem port (modem can be used only by one process "/port> print" )<br>Default: ( unknown ))<br>receive-enabled  (y Must be turned on to receive messages<br>es | no; Default:  no )<br>secret  (string;  the secret password, mandatory<br>Default: "")<br>polling  (yes | no;  checking the modem for new SMS every 10s, instead of updating the inbox only after receiving the command from the modem.<br>Default:  no ) Available starting from v7.16<br>**----- End of picture text -----**<br>

Basic Example configuration to be able to view received messages: 

```
/tool sms set receive-enabled=yes port=lte1
```

```
/tool/sms/print
           status: running
  receive-enabled: yes
             port: lte1
          channel: 0
           secret:
   allowed-number:
       auto-erase: no
          sim-pin:
        last-ussd:
```
