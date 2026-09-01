# Network Identification

## IP address breakdown

(`192.168.100.10/24`)

```
 192 . 168 . 100  .  10   /   24
└───────┬───────┘   └─┬─┘    └─┬─┘
  Network Part     Host ID  Subnet Mask
 (Subnet Group)  (Machine)   (Boundary)
```
| Component | Value | Explanation |
| :--- | :--- | :--- |
| **IP Address** | `192.168.100.10` | full address of this machine |
| **Subnet Mask** | `/24` | rule: The first 3 numbers set the group |
| **Subnet** | `192.168.100.0` | the group. all machine starting with `192.168.100` can talk |
| **Host ID** | `.10` | unique number for this single machine |
