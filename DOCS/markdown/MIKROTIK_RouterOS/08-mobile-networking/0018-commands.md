## Commands 

**==> picture [516 x 241] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>deactivate Deactivate (disable) eSIM profile.<br>/interface/lte/esim deactivate number=0<br>activate Activate (enable) eSIM profile.<br>/interface/lte/esim activate number=0<br>delete Permanently deletes eSIM profile from the eSIM card.<br>/interface/lte/esim delete number=0<br>print List the eSIM profiles installed on eSIM<br>/interface/lte esim print<br>Flags: A - ACTIVE<br>Columns: INTERFACE, NAME, SPN, ICCID, NICKNAME<br>#   INTERFACE  NAME           SPN                   ICCID   NICKNAME<br>0 A lte1       NAME1          SPN1    1111111111111111111   nickname1<br>1   lte1       NAME2          SPN2    2222222222222222222   nickname2<br>2   lte1       NAME3          SPN3    3333333333333333333   nickname3<br>**----- End of picture text -----**<br>

812 

provision Provision new eSIM profile. The command takes four parameters: interface - the interface for which the eSIM profile will be enabled. matching-id - an activation code token. Example:  matching-id=ABCD10EFGHI5KL6M sm-dp-plus - SM-DP+ server hostname confirmation-code - confirmation code (a one-time password that is required in some cases) activate - Activate newly created profile after it is provisioned (yes|no; default: yes) [Available starting from 7.20beta6 version. Before 7.20beta6 profiles do not get activated by default after provisioning.] 

Example eSIM LPA string decoded from QR: LPA:1$server.example.io$ABCD10EFGHI5KL6M 

`/interface/lte/esim provision interface=lte1 sm-dp-plus=` **`server.example.io`** `matching-id=` **`ABCD10EFGHI5KL6M`** esim-id Query the eSIM ID. The command takes one parameter: interface - select the interface for which to query the eSIM ID. `/interface/lte/esim esim-id interface=lte1 eid: 8903302342630000000004181FFFFFFF` setSet a nickname for an eSIM profile. nickname `/interface/lte/esim set-nickname number=0 nickname=nickname1` refreshRe-query the eSIM profile list. The command takes one parameter: profile-list interface - Select an interface for which the eSIM profiles will be re-queried.
