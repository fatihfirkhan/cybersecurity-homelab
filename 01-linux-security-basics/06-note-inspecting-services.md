# Inspecting System Services: `systemd`

Services (daemons) are background programs that run silently without requiring an active terminal window or direct user interaction.

---

## 1. List Loaded Services

List all loaded service units across the system:

`systemctl --type=service --state=running`

**Purpose**: Filters systemd units to display only running service programs (ignoring devices, mount points, timers, and sockets)

---

## 2. Investigating a Specific Service

Inspect the runtime state, process tree, and recent logs of the target service:

`systemctl status cron` <-- investigate system=cron

Output Interpretation:
```
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Sun 2026-08-23 08:11:22 EDT; 4 days ago
   Main PID: 563 (cron)
     Memory: 864K (peak: 2.1M)
        CPU: 691ms
     CGroup: /system.slice/cron.service
             └─563 /usr/sbin/cron -f
```
- State & Uptime (Active: active (running)): Confirms the daemon is healthy and running continuously.

- Boot Configuration (Loaded: ...; enabled;): Confirms the service is set to start automatically at system boot.

- Main PID (Main PID: 563): The primary Process ID tracked by the Linux kernel.

- Resources (Memory: 864K, CPU: 691ms): System resources currently consumed by this process in RAM and CPU time.

- Executed Command (CGroup: └─563 /usr/sbin/cron -f): The exact binary file path and flags used to spawn the service.

- Recent Logs: Real-time log entries at the bottom showing scheduled jobs executed (e.g., automated system accounting scripts and PHP session cleanups).

---

## 3. Extra: Managing and Starting a Service

### 3.1 Check Initial Status

`systemctl status ssh`

Result: `Active: inactive (dead)` and `Loaded: ...; disabled` — SSH server is installed but currently turned off and will not start on boot

### 3.2 Start the SSH Service

Starting services requires administrative privileges

`sudo systemctl start ssh`

### 3.3 Investigate SSH service

`systemctl status ssh`

```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: disabled)
     Active: active (running) since Thu 2026-08-27 09:45:31 EDT; 5s ago
   Main PID: 133276 (sshd)
     Memory: 2M (peak: 2.5M)
        CPU: 32ms
     CGroup: /system.slice/ssh.service
             └─133276 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Aug 27 09:45:31 kali sshd[133276]: Server listening on 0.0.0.0 port 22.
Aug 27 09:45:31 kali sshd[133276]: Server listening on :: port 22.
```
- Active: active (running): SSH server is successfully up and running.

- Main PID: 133276: The SSH daemon is assigned a new process ID.

- Logs (Server listening on 0.0.0.0 port 22): Confirms SSH is actively listening for incoming remote connections on port 22 for both IPv4 and IPv6 (::).

- disabled flag: The service is running right now, but because it is disabled, it will turn back off after the next system reboot.
