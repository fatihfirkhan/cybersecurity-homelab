# Linux System Logs

Exploring how to view auth, sys and kernel logs in terminal

---

## 1.0 Commands

`journalctl` to read event logs from system

---

### 1.1 Common commands

#### View Authentication & Login Logs (Replaces auth.log)
`sudo journalctl -u ssh -n 20`

#### View General System Logs (Replaces syslog)
`sudo journalctl -n 20`

#### View Kernel Logs (Replaces kern.log)
`sudo journalctl -k  -n 20`

---

### 1.2 Flags
`-u` <service>: View logs for a specific systemd service 

`-k`: Shows only kernel-level ring-buffer messages

`-n` <number>: View the last **N** lines

`-f`: Follow logs in real-time (live monitoring)

---

### Note 
```
-n <number> shows only the last <number> log entries. Its optional
```
---

## 2.0 Logs Interpretation

### Sample output
```
Aug 27 09:45:30 kali systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Aug 27 09:45:31 kali sshd[133276]: Server listening on 0.0.0.0 port 22.
Aug 27 09:45:31 kali sshd[133276]: Server listening on :: port 22.
Aug 27 09:45:31 kali systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
```
### How to read the logs?
| timestamp | hostname | Process/Service[PID] | Message |
| --- | --- | --- | --- |
| Aug 27 09:45:30 | kali | systemd[1]: | Starting ssh.service - OpenBSD Secure Shell server |

