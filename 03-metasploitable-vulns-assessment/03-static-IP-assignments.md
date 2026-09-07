# Manually Configure IP to VMs

In previous lab, IP assigned to VMs (Kali Linux and Linux Mint) for Adapter 2 are not permanent and will lose and needed to manually be reassigned after rebooting the VMs. To fix this in this lab the static IP will be configured to the VMs to avoid this issue.

### Metasploitable 2 IP configuration

Identify if the network interfaces for adapter 2 is UP by cross checking output from `ifconfig` and `ip addr`. results show interface eth1 is not up and has no IP assgined to it

Used `sudo nano /etc/network/interfaces` to open the interfaces configuration file 

Typed this at the blank space :
```
iface eth1 inet static
    address 192.168.100.3
    netmask 255.255.255.0
```
save and exit Nano

Run `sudo ifup eth1` to bring the interface up
