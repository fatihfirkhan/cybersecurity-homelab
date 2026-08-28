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

### How to read the logs?
| timestamp | hostname | Process/Service[PID] | Message |
| --- | --- | --- | --- |
| Aug 27 09:45:30 | kali | systemd[1]: | Starting ssh.service - OpenBSD Secure Shell server |

### Sample output `sudo journalctl -u ssh -n 20` (auth log)
```
Aug 27 09:45:30 kali systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Aug 27 09:45:31 kali sshd[133276]: Server listening on 0.0.0.0 port 22.
Aug 27 09:45:31 kali sshd[133276]: Server listening on :: port 22.
Aug 27 09:45:31 kali systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
```

### Sample output `sudo journalctl -n 20` (syslog)

```
Aug 28 02:31:41 kali sudo[211940]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
Aug 28 02:34:23 kali sudo[211940]: pam_unix(sudo:session): session closed for user root
Aug 28 02:34:37 kali sudo[213299]:     kali : TTY=pts/0 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/journalctl -u ssh
Aug 28 02:34:37 kali sudo[213299]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
Aug 28 02:34:41 kali sudo[213299]: pam_unix(sudo:session): session closed for user root
Aug 28 02:34:55 kali sudo[213456]:     kali : TTY=pts/0 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/journalctl -u --no-pager
Aug 28 02:34:55 kali sudo[213456]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
Aug 28 02:34:55 kali sudo[213456]: pam_unix(sudo:session): session closed for user root
Aug 28 02:35:01 kali CRON[213521]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Aug 28 02:35:01 kali CRON[213523]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Aug 28 02:35:01 kali CRON[213521]: pam_unix(cron:session): session closed for user root
Aug 28 02:35:08 kali sudo[213591]:     kali : TTY=pts/0 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/journalctl -u ssh --no-pager
Aug 28 02:35:08 kali sudo[213591]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
Aug 28 02:35:08 kali sudo[213591]: pam_unix(sudo:session): session closed for user root
Aug 28 02:35:36 kali virtualbox-guest-utils[617]: 06:35:36.598178 Timer    VBoxDRMClient: push screen layout data of 1 display(s) to DRM stack, fPartialLayout=false, rc=VINF_SUCCESS
Aug 28 02:35:49 kali sudo[213972]:     kali : TTY=pts/0 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/journalctl -u ssh --no-pager
Aug 28 02:35:49 kali sudo[213972]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
Aug 28 02:35:49 kali sudo[213972]: pam_unix(sudo:session): session closed for user root
Aug 28 02:36:20 kali sudo[214303]:     kali : TTY=pts/0 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/journalctl -n 20
Aug 28 02:36:20 kali sudo[214303]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
```

### Sample output `sudo journalctl -k -n 20` (kernel log)

```
Aug 28 01:26:48 kali kernel: 05:26:48.002047 SHCLX11   Shared Clipboard: Converting X11 format index 0x3 to VBox format 0x1 failed, rc=VERR_SHCLPB_NO_DATA
Aug 28 01:26:49 kali kernel: usb 1-1: USB disconnect, device number 5
Aug 28 01:26:49 kali kernel: 05:26:49.361388 control  Session 0 is about to close ...
Aug 28 01:26:49 kali kernel: 05:26:49.385984 control  Stopping all guest processes ...
Aug 28 01:26:49 kali kernel: 05:26:49.388284 control  Closing all guest files ...
Aug 28 01:26:49 kali kernel: 05:26:49.398902 control  vbglR3GuestCtrlDetectPeekGetCancelSupport: Supported (#1)
Aug 28 01:26:49 kali kernel: usb 1-1: new full-speed USB device number 6 using ohci-pci
Aug 28 01:26:50 kali kernel: usb 1-1: New USB device found, idVendor=80ee, idProduct=0021, bcdDevice= 1.00
Aug 28 01:26:50 kali kernel: usb 1-1: New USB device strings: Mfr=1, Product=3, SerialNumber=0
Aug 28 01:26:50 kali kernel: usb 1-1: Product: USB Tablet
Aug 28 01:26:50 kali kernel: usb 1-1: Manufacturer: VirtualBox
Aug 28 01:26:50 kali kernel: e1000: eth0 NIC Link is Down
Aug 28 01:26:50 kali kernel: e1000 0000:00:03.0 eth0: Reset adapter
Aug 28 01:26:50 kali kernel: input: VirtualBox USB Tablet as /devices/pci0000:00/0000:00:06.0/usb1/1-1/1-1:1.0/0003:80EE:0021.0005/input/input12
Aug 28 01:26:50 kali kernel: hid-generic 0003:80EE:0021.0005: input,hidraw0: USB HID v1.10 Mouse [VirtualBox USB Tablet] on usb-0000:00:06.0-1/input0
Aug 28 01:26:52 kali kernel: e1000: eth0 NIC Link is Up 1000 Mbps Full Duplex, Flow Control: RX
Aug 28 02:07:18 kali kernel: 06:07:08.241279 timesync vgsvcTimeSyncWorker: Radical host time change: 2 423 550 000 000ns (HostNow=1 787 897 228 236 000 000 
Aug 28 02:13:41 kali kernel: 06:07:18.250698 timesync vgsvcTimeSyncWorker: Radical guest time change: 2 423 538 698 000ns (GuestNow=1 787 897 238 250 653 00
Aug 28 02:13:41 kali kernel: 06:13:41.246356 SHCLX11   Shared Clipboard: Converting X11 format index 0x1 to VBox format 0x1 failed, rc=VERR_SHCLPB_NO_DATA
Aug 28 02:13:44 kali kernel: 06:13:44.556893 SHCLX11   Shared Clipboard: Converting X11 format index 0x3 to VBox format 0x1 failed, rc=VERR_SHCLPB_NO_DATA
```
---

### Note
`--no-pager` Flag to basically see the whole message in terminal, avoid message getting cut off/truncates

Forces `journalctl` to output raw text directly to standard output (the terminal stream) instead of opening an interactive pager utility (such as `less`).

#### Why Use It:
* Prevents Line Truncation
* Direct Scripting & Piping
* Terminal Scrollback
