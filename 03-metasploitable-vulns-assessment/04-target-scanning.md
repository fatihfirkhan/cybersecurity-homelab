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
