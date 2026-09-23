## Useful Commands
| Command | Description |
|---|---|
| `ifconfig` | displays or configures active network interface settings (IP address, netmask, MAC address) |
| `sudo nano <filename OR file path>` | opens Nano command-line text editor with root privileges to modify system configuration files (like Windows Notepad) |
| `sudo ifup <interface>` | brings a network interface up using its configured settings |
| `nmcli connection show` | lists all saved NetworkManager connection profiles and active interfaces |
| `sudo nmcli connection modify "<connection_name>" <property> <value>` | edits network settings (such as IP address or static/DHCP method) for a specific profile |
| `sudo nmcli connection up "<connection_name>"` | activates or restarts a connection profile to apply newly configured settings |
| `sudo nmap -sn <target IP>` | scan target IP host |
| `sudo nmap -p- <target IP>` | scans all 65,535 TCP ports on the target host instead of just the default top 1,000 common ports |
| `sudo nmap -sV- <target IP>` | checks open ports to find the exact software name and version number |
| `sudo nmap -sC -sV -p- <target IP>` | checks all 65,535 ports for software versions and runs basic built-in tests |


## Terminology
| Word | Description | Remarks |
|---|---|---|
| Static IP | A manually assigned and permanent IP address | Unlike a DHCP-assigned IP, a static IP keeps the machine's address fixed, making it easier to reliably scan the machine |
| Middleware | Software that connects two systems | Examples include web application servers (like Tomcat) or messaging services (like Java RMI) that sit between user interfaces and databases |

## Flags

| Flags | Description |
| --- | --- |
| `-sn` | Ping scan (checks if the machine is turned on without scanning any ports) |
| `-p-` | All ports (scans every port from 1 to 65535 instead of just the top 1,000) |
| `-sV` | Version detection (finds the exact software name and version number running on open ports) |
| `-sC` | Default scripts (runs basic built-in checks to find extra details and common settings) |
