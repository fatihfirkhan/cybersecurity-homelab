# Network Fundamentals Lab

A hands-on networking and protocol analysis lab conducted within an isolated virtual environment, focusing on interface configuration, Layer 2/3 troubleshooting, port discovery, and packet inspection

---

## 1. Objective

* Network identification and IP configuration
* Layer 2 (ARP) and Layer 3 (ICMP) connectivity testing and virtual cable troubleshooting
* Service discovery, socket listening states, and port scanning
* Packet capture and traffic analysis with Wireshark
* Secure remote administration via OpenSSH 

---

## 2. Environment OS

* VM1: Kali Linux
  * RAM: 5 GB
  * Network: Internal Network (`lab-internal-net` - `192.168.100.1`)
  * Role: Testing machine
* VM2: Linux Mint
  * RAM: 2 GB
  * Network: Internal Network (`lab-internal-net` - `192.168.100.2`)
  * Role: Target

*(Detailed VirtualBox adapter settings: see `03-adapter-configuration.md`)*

---

## 3. Main Tools

| Tool | Purpose | Primary Commands / Usage |
| :--- | :--- | :--- |
| `iproute2` | Interface, address, and ARP cache management | `ip addr`, `ip link`, `ip neigh` |
| `iputils-ping` | Layer 3 ICMP echo reachability testing | `ping -c 4 <ip>` |
| `iproute2 (ss)` | Local socket and listening port inspection | `ss -tulpn` |
| `nmap` | Target service and open-port discovery | `nmap -sV -p- <ip>` |
| `OpenSSH` | Secure remote shell deployment | `ssh username@<ip>`, `systemctl status ssh` |
| `Wireshark` | Real-time packet analysis & protocol disassembly | Filters: `icmp`, `arp`, `tcp.port == 22` |

---

## 4. Key Milestones & Practical Execution

1. **IP & Interface Setup:** Set manual static IPs on both VMs (`192.168.100.1` and `192.168.100.2`) and turned the network interfaces up.
2. **Ping & ARP Testing:** Tested connectivity with `ping` and confirmed MAC addresses showed up in the ARP table.
3. **Layer 2 Troubleshooting:** Fixed the `No route to host` / `FAILED` ARP error by switching Promiscuous Mode to `Allow VMs` and reconnecting the VirtualBox virtual cable.
4. **Port Checking:** Saw how closed ports reject connections with `[RST, ACK]` before an active service is running.
5. **SSH Setup & Packet Capture:** Installed OpenSSH on Linux Mint, logged in remotely from Kali, and captured the TCP handshake, key exchange, and encrypted commands in Wireshark.
