I created the topology for the VLAN Implementation Exercise in the lab on eNSP as shown:

**SW1 (LSW1) is connected to:**

- GE0/0/2 ← PC1
- GE0/0/3 ← PC3
- GE0/0/1 ← connects to SW2

**SW2 (LSW2) is connected to:**

- GE0/0/2 ← PC2
- GE0/0/3 ← PC4
- GE0/0/1 ← connects to SW1

---

After I drawing the topology in eNSP and starting the devices, I configured the VLANs on the switches as follows:

**On SW1:**
```
<Huawei>system-view
[Huawei]sysname SW1
[SW1]vlan batch 10 20
[SW1]interface GigabitEthernet 0/0/2
[SW1-GigabitEthernet0/0/2]port link-type access
[SW1-GigabitEthernet0/0/2]port default vlan 10
[SW1]interface GigabitEthernet 0/0/3
[SW1-GigabitEthernet0/0/3]port link-type access
[SW1-GigabitEthernet0/0/3]port default vlan 20
[SW1]interface GigabitEthernet 0/0/1
[SW1-GigabitEthernet0/0/1]port link-type trunk
[SW1-GigabitEthernet0/0/1]port trunk allow-pass vlan 10 20
```

**On SW2:**
```
<Huawei>system-view
[Huawei]sysname SW2
[SW2]vlan batch 10 20
[SW2]interface GigabitEthernet 0/0/2
[SW2-GigabitEthernet0/0/2]port link-type access
[SW2-GigabitEthernet0/0/2]port default vlan 10
[SW2]interface GigabitEthernet 0/0/3
[SW2-GigabitEthernet0/0/3]port link-type access
[SW2-GigabitEthernet0/0/3]port default vlan 20
[SW2]interface GigabitEthernet 0/0/1
[SW2-GigabitEthernet0/0/1]port link-type trunk
[SW2-GigabitEthernet0/0/1]port trunk allow-pass vlan 10 20
```

---

💡 I assigned the following IP addresses to the PCs as required in the lab:

- PC1: 192.168.10.1/24
- PC2: 192.168.10.2/24
- PC3: 192.168.20.1/24
- PC4: 192.168.20.2/24

Then I tested connectivity using ping:

- PC1 ↔ PC2 worked ✅
- PC3 ↔ PC4 worked ✅
- PC1 ↔ PC3 did NOT work (VLAN isolation) ❌

---

![TASK1-1](https://github.com/user-attachments/assets/42e1204d-cf2b-4e53-9032-9845282dec95)

![TASK1-2](https://github.com/user-attachments/assets/9fe1d48b-7f85-4e18-b2cf-9224703f961a)
