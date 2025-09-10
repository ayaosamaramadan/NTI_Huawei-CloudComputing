# **Routing Implementation Exercise**

## **1️⃣ Topology and Addresses**

* **SW1** is connected to PC1, PC2, and SW2  
* **SW2** is connected to PC3 and SW1

| Device | IP Address    | Subnet Mask      | Default Gateway   |
|--------|--------------|------------------|-------------------|
| PC1    | 10.1.10.10   | 255.255.255.0    | 10.1.10.254       |
| PC2    | 10.1.20.10   | 255.255.255.0    | 10.1.20.254       |
| PC3    | 10.1.30.10   | 255.255.255.0    | 10.1.30.254       |

* The link between SW1 and SW2 is on VLAN40 (10.1.40.0/24)

---

## **2️⃣ SW1 Configuration**

```bash
system-view
sysname SW1

vlan batch 10 20 40

interface GigabitEthernet0/0/1
port link-type access
port default vlan 10
quit

interface GigabitEthernet0/0/2
port link-type access
port default vlan 20
quit

interface GigabitEthernet0/0/3
port link-type trunk
port trunk allow-pass vlan 10 20 40
quit

interface Vlanif10
ip address 10.1.10.254 255.255.255.0
quit

interface Vlanif20
ip address 10.1.20.254 255.255.255.0
quit

interface Vlanif40
ip address 10.1.40.1 255.255.255.0
quit

ip route-static 10.1.30.0 24 10.1.40.2
```

---

## **3️⃣ SW2 Configuration**

```bash
system-view
sysname SW2

vlan batch 30 40

interface GigabitEthernet0/0/1
port link-type access
port default vlan 30
quit

interface GigabitEthernet0/0/3
port link-type trunk
port trunk allow-pass vlan 30 40
quit

interface Vlanif30
ip address 10.1.30.254 255.255.255.0
quit

interface Vlanif40
ip address 10.1.40.2 255.255.255.0
quit

ip route-static 10.1.10.0 24 10.1.40.1
ip route-static 10.1.20.0 24 10.1.40.1
```

---

## **4️⃣ PCs Configuration**

| PC  | IP         | Subnet        | Gateway     |
|-----|------------|---------------|-------------|
| PC1 | 10.1.10.10 | 255.255.255.0 | 10.1.10.254 |
| PC2 | 10.1.20.10 | 255.255.255.0 | 10.1.20.254 |
| PC3 | 10.1.30.10 | 255.255.255.0 | 10.1.30.254 |

---

## **5️⃣ Verification Commands**

### **From SW1**

```bash
ping 10.1.10.254
ping 10.1.20.254
ping 10.1.40.1
ping 10.1.30.254
ping 10.1.40.2
```

### **From SW2**

```bash
ping 10.1.30.254
ping 10.1.40.2
ping 10.1.10.254
ping 10.1.20.254
ping 10.1.40.1
```

### **From PC1**

```bash
ping 10.1.10.254
ping 10.1.20.254
ping 10.1.30.10
ping 10.1.40.1
ping 10.1.40.2
```
![TASK2-3](https://github.com/user-attachments/assets/6f5fd2c3-9692-496d-9703-c95ff35c8e6f)

### **From PC2**

```bash
ping 10.1.20.254
ping 10.1.10.254
ping 10.1.30.10
ping 10.1.40.1
ping 10.1.40.2
```

![TASK2-2](https://github.com/user-attachments/assets/bce08be8-0414-4368-9504-7b501ac3f1fa)


### **From PC3**

```bash
ping 10.1.30.254
ping 10.1.10.10
ping 10.1.20.10
ping 10.1.40.1
ping 10.1.40.2
```

![TASK2-1](https://github.com/user-attachments/assets/9f006c8f-6a55-48c6-9fc7-6cbd3e41e5dd)




