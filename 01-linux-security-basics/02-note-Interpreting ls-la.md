# Linux File System & `ls -la` Notes

How to interpret ls -la output

## Understanding `ls -la` Output Columns

Each line in `ls -la` output is broken into 7 distinct fields:

| Permissions | Links | Owner (User) | Group | Size (Bytes) | Last Modified | Name / Target |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `drwxr-xr-x` | `3` | `root` | `root` | `4096` | `Jun 16 10:30` | `alternatives` |
| `-rw-r--r--` | `1` | `root` | `root` | `3822` | `Jun 1 01:06` | `adduser.conf` |
| `lrwxrwxrwx` | `1` | `root` | `root` | `36` | `Jun 16 10:24` | `localtime -> /usr/...` |

---

## Column 1: Permission String Breakdown

The 10-character string at the start defines the file type and access rights:

```text
 d   rwx   r-x   r-x
 |    |     |     |
 |    |     |     +--> 4. Others Permissions (World)
 |    |     +--------> 3. Group Permissions
 |    +--------------> 2. Owner (User) Permissions
 +-------------------> 1. File Type
```
File Types (Character 1):

    d = Directory (folder)

    - = Regular file

    l = Symbolic link (shortcut / pointer)

Permission  (Characters 2-10):

    r = Read permission (view content / list directory)

    w = Write permission (modify file / create/delete within directory)

    x = Execute permission (run script/program / enter directory)

    - = Permission denied
    
---

## Column 2: Hard Link Count (Shortcuts / Pathways)

Think of this number as "How many direct pathways/doors lead to this item"

* **Regular File:** Almost always `1` (one file path pointing to file's data).

* **Directory:** Counts connections to the folder. 
  * Starts at `2` (the folder name + the `.` inside it).
  * Increases by `1` for every subfolder inside.
  * **Formula:** `Subfolder Count = Link Number - 2`

---

## Directory Observations & Takeaways

 /home (User Isolation):

    - /home/kali is set to drwx------ (kali:kali)

    - Only user kali can access this folder; other standard system users are completely blocked

/etc (System Configuration):

    - Most files are set to -rw-r--r-- (root:root)

    - Only root can edit critical system configs, while standard users have read-only access

    - Contains symlinks like localtime -> /usr/share/zoneinfo/America/New_York to define active timezone settings

/var/log (System Logs & Group Delegation):

    - Certain logs (e.g., apache2, mysql, samba) belong to the adm group (drwxr-x--- ... adm)

    - Users in the adm group can read system logs without escalating to full root privileges

Typo Warning:

    - The Linux temporary scratch directory is strictly /tmp (not /temp)
