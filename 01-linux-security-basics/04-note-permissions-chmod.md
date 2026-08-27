# Linux Permissions: Numeric (Octal) Notation with `chmod`

The `chmod` command modifies file and folder permissions using an additive numeric point system.

---

## 1. Permission Point Values

Each permission type has a dedicated base number:

| Permission | Symbol | Value | Description |
| :--- | :---: | :---: | :--- |
| **Read** | `r` | **4** | View file contents / list directory |
| **Write** | `w` | **2** | Modify file / create & delete files in directory |
| **Execute** | `x` | **1** | Run as a program or script / enter directory |
| **None** | `-` | **0** | No permissions allowed |

---

## 2. Calculating Permission Digits

Add the points together to create a single digit (from `0` to `7`) for each entity:

* **7** = $4 + 2 + 1$ $\rightarrow$ `rwx` (Read + Write + Execute)
* **6** = $4 + 2 + 0$ $\rightarrow$ `rw-` (Read + Write)
* **5** = $4 + 0 + 1$ $\rightarrow$ `r-x` (Read + Execute)
* **4** = $4 + 0 + 0$ $\rightarrow$ `r--` (Read only)
* **0** = $0 + 0 + 0$ $\rightarrow$ `---` (No access)

---

## 3. The 3-Digit Format: `[Owner][Group][Others]`

The three digits in a `chmod` command map directly to the three permission groups in order:

```text
       chmod 644 filename
             |||
             ||+---> 3. Others: 4 (r--)
             |+----> 2. Group:  4 (r--)
             +-----> 1. Owner:  6 (rw-)
