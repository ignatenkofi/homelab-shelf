## 2.3 Pull-Up/Pull-Down Information

### 2.3.1 External Pull-Ups

Table 2-1 lists external pull-up resistors and their functionality.

Table 2-1.       External Pull-Up Resistors
                     External Pull-Up/
   Signal Name                                                                   Notes
                        Pull-Down

RESET_N             Pull-up              In X550-BT2 only.

PE_WAKE_N           Pull-up

FLSH_SCK            Pull-down            Should be pulled down for normal operation.

FLSH_SI             Pull-down/Pull-up    Serial data output to the Flash. In the X550-BT2, no need for a pull-up or a
                                         pull-down. In the X550-AT2, when pulled down, IPsec encryption features are
                                         disabled.

SMBD                Pull-up

SMBCLK              Pull-up

SMBALRT_N           Pull-up

NCSI_CLK_IN         Pull-down            Should be pulled down if NC-SI interface is disabled.

NCSI_CRS_DV         Pull-down
                                         Only if NC-SI is unused or set to multi drop configuration.
NCSI_RXD[1:0]       Pull-up

NCSI_TX_EN          Pull-down
                                         Should be pulled down if NC-SI interface is disabled.
NCSI_TXD[1:0]       Pull-down

JTCK                Pull-down

JTDI                Pull-up
                                         These resistors should be connected if JTAG is not used. See Section 2.2.10 for
JTDO                Pull-up
                                         details.
JTMS                Pull-up

JTRST_N             Pull-down

ENCRYPTION_EN       Pull-up              When pulled up, IPsec encryption features are enabled.
