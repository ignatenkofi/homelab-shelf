## `/routing/ospf/area` 

Property Description 

970 

**==> picture [516 x 330] intentionally omitted <==**

**----- Start of picture text -----**<br>
area-id  (IP OSPF area identifier. If the router has networks in more than one area, then an area with area-id=0.0.0.0 (the backbone) must always be<br>address;  present. The backbone always contains all area border routers. The backbone is responsible for distributing routing information between<br>Default:  0. non-backbone areas. The backbone must be contiguous, i.e. there must be no disconnected segments. However, area border routers do<br>0.0.0 ) not need to be physically connected to the backbone - connection to it may be simulated using a virtual link.<br>default- Default cost of injected LSAs into the area. If the value is not set, then stub area type-3 default LSA will not be originated.<br>cost  (integ<br>er; unset)<br>instance  ( Name of the OSPF instance this area belongs to.<br>name; ma<br>ndatory)<br>no- Flag parameter, if set then the area will not flood summary LSAs in the stub area.<br>summaries<br> ()<br>name  (stri the name of the area<br>ng)<br>nssa- The parameter indicates which ABR will be used as a translator from type7 to type5 LSA. Applicable only if area type is NSSA<br>translate  (<br>yes | no |  yes - the router will be always used as a translator<br>candidate) no - the router will never be used as a translator<br>candidate - OSPF elects one of the candidate routers to be a translator<br>type  (defa The area type. Read more on the area types in the OSPF case studies.<br>ult | nssa<br>| stub;<br>Default:  d<br>efault )<br>**----- End of picture text -----**<br>
