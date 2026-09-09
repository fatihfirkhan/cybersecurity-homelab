## Useful Commands
| Command | Description |
|---|---|
| `ifconfig` | displays or configures active network interface settings (IP address, netmask, MAC address) |
| `sudo nano <filename OR file path>` | opens Nano command-line text editor with root privileges to modify system configuration files (like Windows Notepad) |
| `sudo ifup <interface>` | brings a network interface up using its configured settings |
| `nmcli connection show` | lists all saved NetworkManager connection profiles and active interfaces |
| `sudo nmcli connection modify "<connection_name>" <property> <value>` | edits network settings (such as IP address or static/DHCP method) for a specific profile |
| `sudo nmcli connection up "<connection_name>"` | activates or restarts a connection profile to apply newly configured settings |


## Terminology
| Word | Description | Remarks |
|---|---|---|
| Static IP | A manually assigned and permanent IP address | Unlike a DHCP-assigned IP, a static IP keeps the machine's address fixed, making it easier to reliably scan the machine | 

