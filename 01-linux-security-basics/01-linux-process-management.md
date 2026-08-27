# Linux Process Management: `ps aux` and `top`

A process is simply a program in active execution. Every process has an owner (user account), meaning it runs with that user's permissions

---

## 1. Key Commands & When to Use Them

| Command | Type | When to Use? |
| :--- | :--- | :--- |
| `ps aux` | Static Snapshot | Best for quick script lookups, searching for a specific process, or taking a record at a specific moment |
| `ps aux \| less` | Static + Pager | Best when `ps aux` outputs too much text to fit on screen. Allows scrolling up/down and quitting with `q` |
| `top` | Live Dashboard | Best for real-time monitoring (like Windows Task Manager) to spot frozen applications, high CPU spikes, or RAM hogs. `q` to quit |

### Breaking Down `ps aux` Flags:
* `a`: Show processes from all users on the system
* `u`: Display the user/owner, along with detailed CPU and memory statistics
* `x`: Include background processes that aren't attached to an active terminal window

---

## 2. Interpreting the Headers

### `top`

The output is split into two parts: the **Summary Header** (system health) and the **Process Table** (individual programs).

---

#### 1. Top Summary Area (System Overview)

* **Line 1 (Uptime & Load):** Shows how long the PC has been on and the **load average** (system stress over the last 1, 5, and 15 mins).
* **Line 2 (Tasks):** Counts of total programs—broken down into running, sleeping (idle), paused, or dead (zombie).
* **Line 3 (%Cpu):** 
  * `us`: CPU used by your apps.
  * `sy`: CPU used by the OS core.
  * `id`: Idle CPU (higher = less busy).
  * `wa`: CPU waiting on slow disk reads/writes.
* **Line 4 & 5 (RAM & Swap):** Shows total, free, and used memory. `avail` is how much RAM you can actually use for new apps.

#### 2. Process Table Headers

| Column | Meaning | Description |
| :--- | :--- | :--- |
| **PID** | Process ID | The app's unique tracking number. |
| **USER** | Owner | The account running the program (sets its permissions). |
| **PR** | Priority | How urgently the kernel schedules this app. |
| **NI** | Nice Value | Manual priority tweak ($-20$ = highest priority, $+19$ = lowest). |
| **VIRT** | Virtual Memory | Total RAM the app asked to reserve. |
| **RES** | Resident Memory | The **actual physical RAM** the app is using right now. |
| **SHR** | Shared Memory | RAM this app shares with other programs. |
| **S** | Status | App state: `R` (running), `S` (sleeping/idle), `Z` (dead/zombie). |
| **%CPU** | CPU Percent | How much processor power the app is taking right now. |
| **%MEM** | RAM Percent | How much of your total physical RAM the app takes. |
| **TIME+** | Run Time | Total time the CPU spent working on this app. |
| **COMMAND**| Command / App | The name or file path of the running program. |

### `ps aux`

`ps aux` prints a static snapshot of every running process on your system.

---

#### Process Table Headers

| Column | Meaning | Description |
| :--- | :--- | :--- |
| **USER** | Owner | The account running the program (sets its permissions). |
| **PID** | Process ID | The app's unique tracking number. |
| **%CPU** | CPU Percent | How much processor power the app is using right now. |
| **%MEM** | RAM Percent | How much of your physical RAM the app is using right now. |
| **VSZ** | Virtual Size | Total memory space the app asked for (in KB). |
| **RSS** | Resident Size | The **actual physical RAM** the app is using right now (in KB). |
| **TTY** | Terminal | Which terminal window opened it (`?` means running in the background). |
| **STAT** | Status | App state: `R` (running), `S` (sleeping/idle), `Z` (dead/zombie), `T` (stopped). |
| **START** | Start Time | What time (or date) the program was launched. |
| **TIME** | Run Time | Total active time the CPU spent working on this app. |
| **COMMAND** | Command / App | The exact command or file path used to launch the program. |
