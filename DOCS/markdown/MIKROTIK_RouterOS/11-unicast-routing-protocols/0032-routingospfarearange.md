## `/routing/ospf/area/range` 

**==> picture [401 x 110] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>advertise  (yes | no; Default: yes) Whether to create a summary LSA and advertise it to the adjacent areas.<br>area  (name; mandatory) the OSPF area associated with this range<br>cost  (integer [0..4294967295]) the cost of the summary LSA this range will create<br>default - use the largest cost of all routes used (i.e. routes that fall within this range)<br>prefix  (IP prefix; mandatory) the network prefix of this range<br>**----- End of picture text -----**<br>
