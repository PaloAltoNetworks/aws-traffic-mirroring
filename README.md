# Using VM-Series with AWS Traffic Mirroring
This repository provides a sample firewall configuration that you can import into VM-Series. This sample configuration enables the VXLAN tunnel content inspection (TCI) feature to receive packets sent by the AWS Traffic Mirroring service. This will allow you to get [visibility, and detect and respond](https://live.paloaltonetworks.com) to attacks by sending copies of all packets sent/received by your AWS instances to VM-Series without putting the firewall inline. Putting the VM-Series inline with the traffic flow will allow you actually prevent attacks in real-time. You can also use this capability to run a security lifecycle report (SLR) on your public cloud deployment. 


## How To
Steps for setting up AWS Traffic Mirroring
