## Elastic 

**==> picture [13 x 13] intentionally omitted <==**

Some steps might change over time, refer to Elastic's manual to find the most up-to-date steps. 

1.  Log into your Kibana 2.  Open the Fleet section under the main menu 3.  Open the "Agent policies" section 4.  Press "Create agent policy" button to create a new Agent Policy 5.  Give the policy a name, for example, "NetFlow policy", adjust advance settings if required, create the policy 6.  Open your newly created policy by clicking on it's name 7.  Press "Add integration" 8.  Search for "NetfFlow Records" and press "Add NetFlow Records" 9.  Adjust configuration, make sure: 

   - Specify "UDP host to listen on" to the IP address of your server that is going to run the NetFlow Records integration , in this example the address should be "10.0.0.2" 

10.  Save the integration 11.  Press the "Add Elastic Agent to your host" button 12.  Follow the instructions on how to add Elastic Agent to your host 

**==> picture [13 x 13] intentionally omitted <==**

Official Elastic's manual recommends installing the Elastic Agent as Fleet-managed. Consider following the recommendation since managing the agents is easier when they are Fleet-managed. 

13.  Make sure you have opened the NetFlow port on your host and elsewhere in the path from your RouterOS device (10.0.0.1), the default destination port is 2055/UDP. 

14.  Your Elastic Agent is now ready to receive NetFlow data!
