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

### Note 1
```
n -20 shows only the last 20 log entries. Its optional
```
