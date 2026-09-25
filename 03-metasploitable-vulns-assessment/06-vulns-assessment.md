# Vulns Assessment

## Identified possible vulns

Utilized Claude toc scale down the possible vulnerabilities from the nmap scanning, below are the result from Claude: 

### Tier 1 — known CVEs/backdoors:

- 21/tcp vsftpd 2.3.4 — has a well-known backdoor
- 1524/tcp "Metasploitable root shell" — nmap is telling you this is a shell, literally
- 3632/tcp distccd — known RCE
- 6667/6697 UnrealIRCd — known backdoored version
- 8787 Ruby DRb — known RCE
- 5432/3306 old DB versions with known auth/privesc issues

### Tier 2 — old software, likely has CVEs (worth checking version-specific advisories):

- 22 OpenSSH 4.7p1
- 25 Postfix
- 53 BIND 9.4.2
- 80 Apache 2.2.8
- 8180 Tomcat
- 2121 ProFTPD 1.3.1

### Tier 3 — misconfig/exposure risk rather than a specific CVE:

- 111 rpcbind
- 2049 NFS
- 139/445 Samba
- 512-514 r-services
- 5900 VNC (proto 3.3 = weak auth)
- 6000 X11

