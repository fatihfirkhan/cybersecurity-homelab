# Scan Linux Mint from Kali with `nmap`

![File permissions](screenshots/kali-linux_nmap_linux-mint.png)

In the image, it shows output using `nmap` and `nmap -sV` 

`-sV` flag stands for Service Version detection

## Why Both Scans Showed the Same Result

* Both outputs showed 1000 filtered tcp ports (no-response) because Linux Mint has a firewall (UFW/iptables) blocking TCP packets, or no TCP services are exposed on that interface.

* Because Nmap found zero open ports, -sV had nothing to interrogate, causing both scans to finish with the exact same output


