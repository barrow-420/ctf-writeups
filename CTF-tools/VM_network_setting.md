# Virtualization: Bridged, NAT, Host-only - Virtual machine connection types



## Bridged 
![bridged](https://user-images.githubusercontent.com/76433661/136411729-53437cb8-ee56-4623-8000-23c0db717691.png)
A VM appears to other nodes as just another computer on the network. IP address is visible to any other computer on the network. 

Appropriate for mail server, fiel server, etc.

## NAT
![NAT](https://user-images.githubusercontent.com/76433661/136411732-d0f8ead3-7099-409f-8183-28856489d261.png)
The external physical network sees traffic from the virtual machine as if it comes from the host itself.



## Host-Only
![host-only](https://user-images.githubusercontent.com/76433661/136411736-bb500612-3096-45df-8cff-e0d09047dcca.png)
It is appropriate for cyber security experiment.

VMs on the host can only talk with each other and with their host. Cannot communicate with other computers beyond. 

We can avoid leaking our packet to normal network.


Source : https://youtu.be/XCkKDWMYHME
