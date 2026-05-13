## VLAN in a bridge with a physical interface 

Very similar case to VLAN on a bridge in a bridge. The most popular use case is when you want to bridge a physical interface with a VLAN (simplified trunk /access port setup). In such setup you might want to send out tagged traffic on one side and untagged on the other side. To acomplish this, you create a VLAN interface on the trunk port (the tagged side), then create a bridge and add both the VLAN interface and the physical interface (the untagged side) as bridge ports.
