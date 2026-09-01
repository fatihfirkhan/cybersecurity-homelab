## Useful Commands
| Command | Description |
|---|---|
| `ip addr` | N/A |


## Terminology
| Word | Description | Remarks |
|---|---|---|
| NAT | Network Address Translation; shares physical computer’s internet connection with the VM | VM can connect to internet, but other devices on the network cannot see or directly connect to the VM | 
| Host-Only | creates a private network between physical computer (the host) and the VMs | no internet |
| Internal Network | isolated virtual switch only for VMs | host machine cannot see the traffic, and no internet for VMs |
| Outbound traffic | network data that starts inside your machine and goes out to external destination |
| subnet | smaller, isolated section of a larger network | IP address is a street address, the subnet is the specific **neighborhood**. Devices in the same **neighborhood** can talk directly to each other without needing a router |
| DHCP | Dynamic Host Configuration Protocol; service that automatically gives your computer an IP address and other network settings | |
