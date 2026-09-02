# Scan Linux Mint from Kali with `nmap`

![File permissions](screenshots/kali-linux_nmap_linux-mint.png)

In the image, it shows output using `nmap` and `nmap -sV` 

`-sV` flag stands for Service Version detection

## Why Both Scans Showed the Same Result

* Both outputs showed 1000 filtered tcp ports (no-response) because Linux Mint has a firewall (UFW/iptables) blocking TCP packets, or no TCP services are exposed on that interface.

* Because Nmap found zero open ports, -sV had nothing to interrogate, causing both scans to finish with the exact same output

---

## Nmap Scan & Listening Services Analysis

### 1. Scan Results Summary
* **Open Ports:** None found (0 open ports).
* **Services Detected:** None.
* **Scan Output:** All 1,000 scanned TCP ports reported as `filtered (no-response)`.

---

### 2. Comparison: Nmap (Kali) vs. `ss -tulpn` (Linux Mint)

**Question:** Does what Kali sees match what Linux Mint says is listening?

**Answer:** Yes, the results match.

* **TCP Scans vs. UDP Services:** Standard `nmap` checks only TCP ports. Linux Mint's only network-wide service (`avahi-daemon`) runs on **UDP port 5353**, making it invisible to standard scans.
* **Localhost Restrictions:** The TCP services running on Linux Mint (`cupsd` on port 631 and `systemd-resolve` on port 53) are locked to loopback addresses (`127.0.0.1` and `127.0.0.53`). They only accept internal traffic from Linux Mint itself and drop any traffic from Kali.

---

### 3. Why Those Ports Are Not Visible to Kali

| Service | Protocol & Port | Bound Address | Reachable by Kali? | Reason |
| :--- | :--- | :--- | :--- | :--- |
| `cupsd` | TCP 631 | `127.0.0.1` | No | Bound only to internal loopback. |
| `systemd-resolve` | TCP/UDP 53 | `127.0.0.53` | No | Bound only to internal loopback. |
| `avahi-daemon` | UDP 5353 | `0.0.0.0` | Yes (UDP only) | Missed by standard TCP Nmap scan. |


