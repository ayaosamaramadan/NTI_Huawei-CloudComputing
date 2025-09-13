# Linux Permissions Management Task

## 📌 Objective
This task demonstrates how to manage **users, groups, folders, files, ownership, and permissions** in Linux using the `chown`, `chmod`, `useradd`, and `groupadd` commands
on VMware workstation and openEuler.

---

![task1](https://github.com/user-attachments/assets/cceca2c8-24c7-489a-8a0f-323e0cbfca89)

## 🗂️ Folder Structure
i will create a shared directory with multiple subfolders:

```

/share\_drive
├── business-data
├── hr-data
├── marketing-data
└── ops-data

````

---

## 👥 Users & Groups
### Groups
- **Business**
- **HumanReso**
- **Marketing**
- **Design**
- **Engineering**

### Users
- **Jessica** → HumanReso  
- **Tony** → Business, HumanReso, Marketing  
- **Debbie** → Design, Engineering  
- **Stephen** → Engineering  

---

## 📄 Files to Create
- `business-data/`
  - `cost_estimate-2022.csv`
  - `invoices.pdf`
- `hr-data/`
  - `candidates.csv`
  - `employees.txt`
- `marketing-data/`
  - `partners-2022.csv`
- `ops-data/`
  - `prototypes-2022.csv`
  - `eng_drawing.pdf`

---

## ⚙️ Step-by-Step Commands

### 1. Create Folders
```bash
sudo mkdir -p /share_drive/business-data /share_drive/hr-data /share_drive/marketing-data /share_drive/ops-data
````

### 2. Create Groups

```bash
for group in Business HumanReso Marketing Design Engineering; do
    sudo groupadd -f $group
done
```

### 3. Create Users and Add Them to Groups

```bash
sudo useradd -m -G HumanReso Jessica
sudo useradd -m -G Business,HumanReso,Marketing Tony
sudo useradd -m -G Design,Engineering Debbie
sudo useradd -m -G Engineering Stephen
```

### 4. Create Files

```bash
sudo touch /share_drive/business-data/cost_estimate-2022.csv
sudo touch /share_drive/business-data/invoices.pdf
sudo touch /share_drive/hr-data/candidates.csv
sudo touch /share_drive/hr-data/employees.txt
sudo touch /share_drive/marketing-data/partners-2022.csv
sudo touch /share_drive/ops-data/prototypes-2022.csv
sudo touch /share_drive/ops-data/eng_drawing.pdf
```

### 5. Assign Ownership

```bash
sudo chown Tony:Business /share_drive/business-data/*
sudo chown Jessica:HumanReso /share_drive/hr-data/candidates.csv
sudo chown Tony:HumanReso /share_drive/hr-data/employees.txt
sudo chown Marketing:Marketing /share_drive/marketing-data/partners-2022.csv
sudo chown Debbie:Design /share_drive/ops-data/prototypes-2022.csv
sudo chown Stephen:Engineering /share_drive/ops-data/eng_drawing.pdf
```

### 6. Set Permissions (Full Access)

```bash
sudo chmod 777 /share_drive/business-data/*
sudo chmod 777 /share_drive/hr-data/*
sudo chmod 777 /share_drive/marketing-data/*
sudo chmod 777 /share_drive/ops-data/*
```

---

## ✅ Verification

### Check Groups

```bash
groups Jessica
groups Tony
groups Debbie
groups Stephen
```

**Expected Output:**

```
Jessica : Jessica HumanReso
Tony    : Tony Business HumanReso Marketing
Debbie  : Debbie Design Engineering
Stephen : Stephen Engineering
```

---

### Check File Permissions

```bash
ls -l /share_drive/business-data/
ls -l /share_drive/hr-data/
ls -l /share_drive/marketing-data/
ls -l /share_drive/ops-data/
```

**Expected Output Example:**

```
-rwxrwxrwx 1 Tony    Business    0 Sep 14 22:00 cost_estimate-2022.csv
-rwxrwxrwx 1 Tony    Business    0 Sep 14 22:00 invoices.pdf
-rwxrwxrwx 1 Jessica HumanReso   0 Sep 14 22:00 candidates.csv
-rwxrwxrwx 1 Tony    HumanReso   0 Sep 14 22:00 employees.txt
-rwxrwxrwx 1 Marketing Marketing 0 Sep 14 22:00 partners-2022.csv
-rwxrwxrwx 1 Debbie  Design      0 Sep 14 22:00 prototypes-2022.csv
-rwxrwxrwx 1 Stephen Engineering 0 Sep 14 22:00 eng_drawing.pdf
```
