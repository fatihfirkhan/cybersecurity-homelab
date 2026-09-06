# Adapter Configurations
This section provide details of the network adapters used for the project

* Adapter 1
  * NAT
  * Used for internet access

* Adapter 2
  * Internal Network
  * Used for communication between Kali and Linux Mint

## Internal Network Adapter Setup
* Kali Linux
  * name: lab-internal-net
  * adapter type: Intel PRO/1000 MT Desktop (82540EM)
  * Promiscuous Mode: Allow all
  * interface: eth1
 
* Linux Mint
  * name: lab-internal-net
  * adapter type: Intel PRO/1000 MT Desktop (82540EM)
  * Promiscuous Mode: Deny $\rightarrow$ Allow VMs (Refer to ![08-note-ssh-service_and_layer2-troubleshooting.md](08-note-ssh-service_and_layer2-troubleshooting.md))
  * interface: enp0s8
 
* Subnet: `192.168.100.0/24`
