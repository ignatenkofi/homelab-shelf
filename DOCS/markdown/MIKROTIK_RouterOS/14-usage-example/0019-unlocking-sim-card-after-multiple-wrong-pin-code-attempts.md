## Unlocking SIM card after multiple wrong PIN code attempts 

After locking the SIM card, unlock can be done through "at-chat" 

Check current PIN code status: 

```
/interface lte at-chat lte1 input="at+cpin\?"
```

If card is locked - unlock it by providing: 

```
/interface lte at-chat lte1 input="AT+CPIN=\"PUK_code\",\"NEW_PIN\""
```

Replace PUK_code and NEW_PIN with matching values. 

**==> picture [13 x 13] intentionally omitted <==**

The command for sim slot selection changes in v6.45.1 and again in v7. Some device models like SXT, have SIM slots named "a" and "b" instead of "up" and down" 

825
