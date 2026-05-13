## Read-only properties 

**==> picture [516 x 99] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>in-errors  (integer) All inbound errors that are not matched by other counters.<br>in-buffer-errors  (integer) No free buffer.<br>in-header-errors  (integer) Header error.<br>in-no-states  (integer) No state is found i.e. either inbound SPI, address, or IPsec protocol at SA is wrong.<br>**----- End of picture text -----**<br>


1195 

**==> picture [516 x 492] intentionally omitted <==**

**----- Start of picture text -----**<br>
in-state-protocol-errors  (int Transformation protocol-specific error, for example, SA key is wrong or hardware accelerator is unable to handle the<br>eger) number of packets.<br>in-state-mode-errors  (integ Transformation mode-specific error.<br>er)<br>in-state-sequence-errors  (i A sequence number is out of a window.<br>nteger)<br>in-state-expired  (integer) The state is expired.<br>in-state-mismatches  (integ The state has a mismatched option, for example, the UDP encapsulation type is mismatched.<br>er)<br>in-state-invalid  (integer) The state is invalid.<br>in-template-mismatches  (i No matching template for states, e.g. inbound SAs are correct but the SP rule is wrong. A possible cause is a mismatched<br>nteger) sa-source or sa-destination address.<br>in-no-policies  (integer) No policy is found for states, e.g. inbound SAs are correct but no SP is found.<br>in-policy-blocked  (integer) Policy discards.<br>in-policy-errors  (integer) Policy errors.<br>out-errors  (integer) All outbound errors that are not matched by other counters.<br>out-bundle-errors  (integer) Bundle generation error.<br>out-bundle-check-errors  (i Bundle check error.<br>nteger)<br>out-no-states  (integer) No state is found.<br>out-state-protocol-errors  (i Transformation protocol specific error.<br>nteger)<br>out-state-mode-errors  (int Transformation mode-specific error.<br>eger)<br>out-state-sequence-errors Sequence errors, for example, sequence number overflow.<br>(integer)<br>out-state-expired  (integer) The state is expired.<br>out-policy-blocked  (integer) Policy discards.<br>out-policy-dead  (integer) The policy is dead.<br>out-policy-errors  (integer) Policy error.<br>**----- End of picture text -----**<br>
