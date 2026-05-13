## Sorting out displayed items 

Almost every window has a Sort button. When clicking on this button several options appear as illustrated in the screenshot below 

264 

**==> picture [434 x 272] intentionally omitted <==**

The example shows how to quickly filter out routes that are in the 10.0.0.0/8 range 

1. Press Sort button 

2. Choose Dst.Address from the first drop-down box. 3. Choose  form the second drop-down box. "in" means that filter will check if DST address value is in range of the specified network. in 

4. Enter the network against which values will be compared (in our example enter "10.0.0.0/8") 

5. These buttons are to add or remove another filter to the stack. 

6. Press the Filter button to apply our filter. 

As you can see from the screenshot WinBox sorted out only routes that are within the 10.0.0.0/8 range. 

Comparison operators (Number  in the screenshot) may be different for each window. For example "IP Route" window has only two  and . Other 3 is in windows may have operators such as "is not", "contains", "contains not". 

WinBox allows building a stack of filters. For example, if there is a need to filter by destination address and gateway, then 

set the first filter as described in the example above, 

- press [+] button to add another filter bar in the stack. set up a second filter to filter by the gateway 

- press the Filter button to apply filters. 

You can also remove unnecessary filters from the stack by pressing the [-] button.
