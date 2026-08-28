# Network Ports

virtual communication endpoints that direct incoming and outgoing network traffic to the specific service or application running on a device

## 1.0 SSH

SSH (Secure Shell) is a **network protocol** that allows you to securely connect to, control, and execute commands on a remote computer or server over an unsecured network

### How It Works

- Client-Server Architecture:

  - The SSH Server (the `sshd` service you turned on earlier) runs in the background on the remote machine, listening for incoming connection requests (default: Port 22)

  - The SSH Client is the program on your local machine used to initiate the connection (e.g., typing ssh user@remote_ip in your terminal)

- End-to-End Encryption: Every piece of data sent across the connection—including commands, typed passwords, and terminal output—is encrypted, preventing eavesdropping, tampering, or man-in-the-middle attacks

### Primary Uses

- **Remote Administration**: Logging into remote Linux/Unix servers or virtual machines from anywhere to manage files and execute terminal commands

- **Secure File Transfers**: Transferring files securely using protocols built on top of SSH, such as SCP and SFTP

- **Port Forwarding & Tunneling**: Creating an encrypted "tunnel" through which other non-secure network traffic can flow safely

- **Git Version Control**: Authenticating securely with repositories on platforms like GitHub/GitLab using SSH key pairs rather than passwords

---

## 2.0 Ports

a **virtual doorway** on a computer that directs incoming and outgoing internet traffic to the correct software or service

### How to Think About Ports (The Apartment Analogy)

- IP Address = Street Address: Directs the network traffic to your specific computer or server

- Port Number = Apartment Number: Directs the traffic to the specific application running inside that computer

Without port numbers, your computer wont know whether **incoming network data** is meant for your **web browser, your SSH server, a video game, or an email client**

### Essential Standard Ports to Know
| Port | Protocol | What is it for |
| --- | --- | --- |
| 20 / 21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure terminal remote access |
| 25 | SMTP | Send email |
| 53 | DNS | Domain name resolution (converting domain names to IP addresses) |
| 80 | HTTP | Unencrypted web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 3306 | MySQL | MySQL database connections |
| 3389 | RDP | Remote Desktop Protocol (Windows remote desktop) |

---

## 3.0 `ss` command

ss is used to inspect network connections, open ports, and socket performance

The Essential Command: `ss -tuln` AND `sudo ss -tulpn` 

- `-tulpn` flags gives a clear list of every service currently listening on your machine

  - `t` (**TCP**): Show TCP sockets (reliable, connection-oriented protocols like HTTP, SSH, HTTPS)

  - `u` (**UDP**): Show UDP sockets (lightweight, connectionless protocols like DNS, DHCP, streaming)

  - `l` (**Listening**): Only show **Listening** sockets

  - `p` (**Processes**): Show the process name and PID using the socket (requires sudo)

  - `n` (**Numeric**): Output raw IP addresses and port numbers instead of resolving them to names (e.g., shows 22 instead of ssh, and 80 instead of http)
 
### `ss -tuln` Output Interpretation

| Netid | State | Recv-Q | Send-Q | Local Address:Port | Peer Address:Port |
| --- | --- | --- | --- | --- | --- |
| tcp | LISTEN | 0 | 128 | 0.0.0.0:22 | 0.0.0.0:* |     
| tcp | LISTEN | 0 | 128 | [::]:22 | [::]:* |

Output Breakdown:

- **Netid** (tcp): The socket uses the reliable, connection-based TCP protocol

- **State** (LISTEN): The port is open and waiting on standby for incoming connection attempts

- **Recv-Q** / **Send-Q**:

  - **Recv-Q** (0): Current number of incoming connection requests waiting in the queue (Currently 0)

  - **Send-Q** (128): Maximum backlog size (up to 128 pending connection requests can wait in queue before new ones get dropped)

- **Local Address:Port**:

  - **0.0.0.0:22**: The service is listening on Port 22 across all available IPv4 network interfaces (Ethernet, Wi-Fi, loopback)

  - **[::]:22**: The service is listening on Port 22 across all available IPv6 network interfaces

- **Peer Address:Port** (0.0.0.0:* / [::]:*): Shows the remote client address. The * wildcard indicates that any remote client can connect, but no active session is connected yet
