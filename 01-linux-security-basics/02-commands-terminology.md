## Useful Commands
| Command | Description |
|---|---|
| `whoami` | which user account currently operating |
| `id` | user detailed information |
| `groups` | shows which groups current user belongs to|
| `ls` | list |
| `Ctrl + L` | clear terminal |
| `pwd` | Print Working Directory; shows full path of the folder you are currently in |
| `cd -` | undo to previous directory |
| `cd ~` | return to home directory |
| `mkdir` | create new directory/folder |
| `echo` | prints text to screen or sends text into a file |
| `chmod` | changes a file's permissions |
| `su` | switch user; temporarily switches to another user account in the terminal |
| `cat` | reads, displays, and concatenates file contents to the terminal |
| `systemctl`  | used to control background programs (services) on Linux. Think of it as the On/Off/Restart switch for tools like SSH, web servers, or firewalls |
| `ss` | socket statistics; | inspect network connections, open ports, and socket performance |
| `sudo apt update && sudo apt install` | update & install software applications |

## Terminology
| Word | Description |
|---|---|
| Auto-mount | automatically make the shared folder available every time Kali starts |
| Make Permanent | save shared-folder configuration |
| groups | collection of user accounts bundled together to share same permissions & access rights |
| flags | options/switches that modify how the command behaves (e.g., -l or -a) *refer **ls-la_command.png**  |
| symlink | symbolic link; basically a shortcut file |
| service | also called a daemon; program that runs silently in the background without needing an open window or user interaction |
| SSH | Secure Shell; network protocol that allows to securely connect, control, and execute commands on a remote computer/server over an unsecured network |
| ports | virtual doorway that directs incoming and outgoing internet traffic to the correct software/service |
| Listening | program is on standby, waiting for incoming data or a connection |


## Flags
| Flags | Description |
|---|---|
| `-l` | Long format (shows file permissions, owner, size, and date modified) |
| `-a` | All (shows hidden files that start with a dot (e.g., bashrc) |
| `--type=service` | Look only at services (ignores hardware mounts, timers, sockets) |
| `--state=running` | Only displays processes currently alive in memory |


## Root-level directories in Linux
| Directory | Description |
|---|---|
| /home | Personal folders for regular users |
| /etc | System-wide config and settings files |
| /var | Variable data that changes during system operation (system logs, mail spools, and databases) |
| /tmp | Temporary files |
| /usr | User programs, tools, and libraries that come with the os |
| /opt | Optional, self-contained third-party software |


## Key Group Permissions for kali
| Group | Description |
|---|---|
| sudo | lets you run administrator commands |
| wireshark | capture network traffic without needing full admin rights |
| vboxsf | lets you access shared folders between VirtualBox and your virtual machine |
| adm | Grants read permissions to system log files located in /var/log |
| netdev | Lets you configure Wi-Fi and network connections via NetworkManager without root escalation |
| kaboxer | Lets you run Kali apps isolated inside lightweight containers |
| audio, video, bluetooth, plugdev, dialout | Provide direct hardware access to audio devices, displays/webcams, Bluetooth adapters, removable storage drives, and serial/modem communication ports |
