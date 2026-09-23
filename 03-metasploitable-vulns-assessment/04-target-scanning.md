# Metasaploitable 2 Scanning from Kali Linux

## 1.0 Host Discovery

run `sudo nmap -sn <target IP>` in Kali Linux

Result:

```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sn 192.168.100.3
[sudo] password for kali: 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-10 01:17 -0400
Nmap scan report for 192.168.100.3 (192.168.100.3)
Host is up (0.015s latency).
MAC Address: 08:00:27:0E:0A:C0 (Oracle VirtualBox virtual NIC)
Nmap done: 1 IP address (1 host up) scanned in 2.11 seconds
```

In this context: The host is specifically the Metasploitable 2 target at 192.168.100.3 and the result indicates the host is alive by `Host is up (0.015s latency).`

## 2.0 Basic Port Scanning

run `sudo nmap <target IP>` in Kali Linux

Result:

```
┌──(kali㉿kali)-[~]
└─$ sudo nmap 192.168.100.3    
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-10 01:27 -0400
Stats: 0:00:02 elapsed; 0 hosts completed (0 up), 1 undergoing ARP Ping Scan
Parallel DNS resolution of 1 host. Timing: About 0.00% done
Nmap scan report for 192.168.100.3 (192.168.100.3)
Host is up (0.0019s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 08:00:27:0E:0A:C0 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 2.60 seconds
```
### Scan Highlights

    Total Ports Scanned: Top 1,000 TCP ports

    State: 977 closed ports, 23 open ports

    Target Host Latency: 0.0019s (confirming high responsiveness on local network)

### Port and Service Analysis

The 23 open ports identified represent a massive attack surface across various functional categories:
A. Core Web & Application Services

    Port 80 (HTTP): Serves web pages and web applications hosted on Apache

    Port 8009 (AJP13) & Port 8180 (HTTP Alternate): Apache JServ Protocol and secondary web port used for directing traffic to an Apache Tomcat web container

B. Remote Access & Management

    Port 22 (SSH): Standard secure remote CLI administration

    Port 23 (Telnet): Legacy unencrypted remote command-line login (cleartext risk)

    Port 5900 (VNC) & Port 6000 (X11): Remote graphical display systems (virtual desktop access)

    Ports 512, 513, 514 (BSD 'r' services - rexec, rlogin, rsh): Obsolete Unix remote execution services that typically rely on insecure host-trust relationships without strong authentication

C. File Sharing & Network Infrastructure

    Port 21 (FTP) & Port 2121 (FTP Alternate): Used for bi-directional file transfer between systems

    Port 53 (DNS / Domain): Local domain name resolution service

    Port 111 (rpcbind) & Port 2049 (NFS): Remote Procedure Call and Network File System used to mount remote file systems over the network

    Port 139 & 445 (NetBIOS-SSN & SMB): Windows-compatible file and print sharing protocols (Samba)

D. Mail & Communication

    Port 25 (SMTP): Simple Mail Transfer Protocol used for mail delivery and routing

    Port 6667 (IRC): Internet Relay Chat daemon hosting real-time text chat channels

E. Database Management Systems

    Port 3306 (MySQL): Relational database backend typically paired with the port 80 web applications

    Port 5432 (PostgreSQL): Secondary relational database management system

F. Middleware & Suspicious Ports

    Port 1099 (Java RMI Registry): Remote Method Invocation service allowing Java objects to execute calls across the network

    Port 1524 (ingreslock): Historically an Ingres database port, but frequently associated with legacy root shell backdoors


## 3.0 Scan All TCP Ports

The default Nmap scan does not necessarily scan every TCP port

run `sudo nmap -p- <target IP>` in Kali Linux

Result:

```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -p- 192.168.100.3
[sudo] password for kali: 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-14 09:13 -0400
Nmap scan report for 192.168.100.3 (192.168.100.3)
Host is up (0.0036s latency).
Not shown: 65505 closed tcp ports (reset)
PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
23/tcp    open  telnet
25/tcp    open  smtp
53/tcp    open  domain
80/tcp    open  http
111/tcp   open  rpcbind
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
512/tcp   open  exec
513/tcp   open  login
514/tcp   open  shell
1099/tcp  open  rmiregistry
1524/tcp  open  ingreslock
2049/tcp  open  nfs
2121/tcp  open  ccproxy-ftp
3306/tcp  open  mysql
3632/tcp  open  distccd
5432/tcp  open  postgresql
5900/tcp  open  vnc
6000/tcp  open  X11
6667/tcp  open  irc
6697/tcp  open  ircs-u
8009/tcp  open  ajp13
8180/tcp  open  unknown
8787/tcp  open  msgsrvr
48213/tcp open  unknown
48323/tcp open  unknown
50823/tcp open  unknown
52385/tcp open  unknown
MAC Address: 08:00:27:0E:0A:C0 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 32.19 seconds
```
### Analysis & Comparison

    Initial Scan (Top 1,000 Ports): 23 open ports detected

    Full Port Scan (Ports 1–65535): 30 open ports detected

    Delta: 7 additional open ports discovered

### Newly Identified Ports

    Port 3632 (distccd): A distributed compilation daemon known to be a frequent vector for remote code execution if misconfigured

    Port 6697 (ircs-u): Encrypted IRC daemon port

    Port 8787 (msgsrvr): Non-standard messaging server port

    Ports 48213, 48323, 50823, 52385 (unknown / RPC services): Dynamic high ports opened by RPC-related daemons (such as NFS/status/lockd) via rpcbind

## 4.0 Service and Version Detection

The default Nmap scan does not necessarily scan every TCP port

run `sudo nmap -sV <target IP>` in Kali Linux; This tells Nmap to attempt to identify:

- Service
- Product
- Version

Result:

```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -sV 192.168.100.3
[sudo] password for kali: 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-14 09:28 -0400
Nmap scan report for 192.168.100.3 (192.168.100.3)
Host is up (0.015s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec?
513/tcp  open  login       OpenBSD or Solaris rlogind
514/tcp  open  tcpwrapped
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
MAC Address: 08:00:27:0E:0A:C0 (Oracle VirtualBox virtual NIC)
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 83.04 seconds
```
Running `nmap -sV` revealed that the target is running ancient, unpatched software from around 2008–2011. Instead of generic services, specific versions were identified and categorized by risk:

### A. Critical Backdoors & Immediate Compromise Risks
* **Port 1524 (bindshell / Metasploitable root shell):** A raw command shell running directly as root. Anyone who connects gets instant full administrative control without needing a password
* **Port 21 (vsftpd 2.3.4):** A famously compromised release that contains a malicious backdoor (CVE-2011-2523), allowing attackers to gain a root shell
* **Port 6667 (UnrealIRCd):** An IRC chat service running a backdoored version (CVE-2010-2075) that allows arbitrary system command execution

### B. Unencrypted Legacy Protocols (Cleartext Risk)
* **Port 23 (Telnet) & Ports 512–514 (BSD 'r' services):** Obsolete administrative protocols that send all credentials and commands in clear, unencrypted text across the wire
* **Port 21 / 2121 (FTP - vsftpd & ProFTPD 1.3.1):** File transfer services that pass usernames and passwords in plain text

### C. Outdated Core Services & Exposed Databases
* **Port 80 (Apache httpd 2.2.8) & Port 8180 (Apache Tomcat 1.1):** Severely outdated web servers and servlet engines frequently targeted for default credentials and arbitrary code execution
* **Port 3306 (MySQL 5.0.51a) & Port 5432 (PostgreSQL 8.3):** Old database management systems exposed directly to the network instead of being isolated locally
* **Port 139 / 445 (Samba 3.X):** Legacy file-sharing daemon with known vulnerabilities for remote execution

### Summary
Version detection proves that vulnerabilities do not stem from the port numbers themselves, but from obsolete and backdoored software versions (e.g., `vsftpd 2.3.4` vs standard modern FTP)

## 5.0 Run Nmap Default Scripts

The default Nmap scan does not necessarily scan every TCP port

run `sudo nmap -sC -sV -p- <target IP>` in Kali Linux; This tells Nmap to attempt to identify:
```
-p-
↓
Find all ports

-sV
↓
Identify services/versions

-sC
↓
Gather additional information
```
Result:
![Nmap Full Scan](screenshots/nmap-full-enum.txt)

*The full scan output was saved directly to a text file due to terminal length limits:*
