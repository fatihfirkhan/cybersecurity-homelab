# Metasaploitable 2 Scanning from Kali Linux

## 1.0 Host Discovery

run `sudo nmap -sn <target IP>` in Kali Linux

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
