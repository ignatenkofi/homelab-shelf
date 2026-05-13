## <802.11 reason> and <802.11 status> 

These are numeric reason/status codes encoded into 802.11 management messages. Log messages include numeric code and textual description from appropriate standard in 802.11 standards group. Although these are intended to be as descriptive as possible, it must be taken into account that actual reason/status code that appears in management frames depends solely on equipment or software manufacturer - where one device sends 802.11 management frame including proper reason/status code for situation that caused the frame, other may send frame with "unspecified" reason/status code. Therefore reason/status code should only be considered informational. 

As 802.11 standards evolve, RouterOS may miss textual descriptions for reason/status codes that some devices use. In such case numeric value should be used to lookup meaning in 802.11 standards. 

In order to properly interpret reason/status code, good understanding of 802.11 group standards is necessary. Most of the textual descriptions are selfexplaining. Explanation for some of most commonly seen reson/status codes follows. 

class 2 frame received (6) - device received "class 2" frame (association/reassociation management frame) before completing 802.11 authentication process; 

class 3 frame received (7) - device received "class 3" frame (data frame) before completing association process;
