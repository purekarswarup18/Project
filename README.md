# 🧑‍💻 IT Support Lab — Active Directory & Windows Server Setup

## 📘 Overview
This virtual lab was created to simulate a small corporate IT environment.  
It includes:
- **Windows Server 2019 (Domain Controller)**
- **Windows 10 (Helpdesk Client)**

The goal was to practice **Active Directory management, Group Policy, user permissions, password resets, and troubleshooting** in a real-world environment.

---

## 🏗 Lab Environment

| Component | Description |
|------------|-------------|
| Hypervisor | Oracle VirtualBox |
| Domain Controller | Windows Server 2019 |
| Client Machine | Windows 10 |
| Network Type | Host-Only Adapter |
| Domain Name | `purekarlab.local` |

---

## ⚙️ Step 1: Create and Configure Virtual Machines

### 1.1 VirtualBox Setup
- Created two VMs:  
  - `DC01` — Windows Server 2019  
  - `HELPDESK01` — Windows 10 Pro  
- Both configured with Host-Only network for internal communication.

📸 **Screenshot:**  
![Image](https://github.com/user-attachments/assets/c459de87-8020-481c-945c-a417c772837d)

---


## 🧱 Step 2: Install Active Directory & DNS

1. Open **Server Manager → Add Roles and Features**.  
2. Install **Active Directory Domain Services (AD DS)** and **DNS Server**.  
3. Promote the server to a **Domain Controller** (`purekarlab.local`).

📸 **Screenshot:**  

![Image](https://github.com/user-attachments/assets/628974fb-4b34-4cf4-b436-b6a704ca781c)

![Image](https://github.com/user-attachments/assets/e96a124c-074a-49e1-b59a-27945c66424e)

![Image](https://github.com/user-attachments/assets/2fb3d51d-d888-4429-b442-28fc8b0eb0e9)

![Image](https://github.com/user-attachments/assets/1e887b2e-27a2-4aa6-8397-677086647c08)






---

## 👥 Step 3: Create Users & Organizational Units (OUs)

1. Open **Active Directory Users and Computers (ADUC)**.  
2. Created OUs:
   - `IT`
   - `HR`
   - `Helpdesk`
3. Created test users:  
   - `helpdesk.user`
   - `it.admin`

📸 **Screenshot:**  
![Image](https://github.com/user-attachments/assets/e10ece62-fae5-4c09-b982-6ff13d80e6ac)

![Image](https://github.com/user-attachments/assets/727c7267-fd24-4e26-849c-5a21df018ec3)

![Image](https://github.com/user-attachments/assets/e34dd70f-a902-4149-b1e0-deef31a63667)

![Image](https://github.com/user-attachments/assets/c7d460a0-bfb5-40c4-bdcc-597ee43734ab)

![Image](https://github.com/user-attachments/assets/3bbf88e1-137e-492a-ae85-b8c780c83a04)


## 🧩 Step 4: Apply Group Policies

1. Open **Group Policy Management Console**.  
2. Created and linked a GPO named **PasswordPolicy**:
   - Minimum password length = 8  
   - Maximum password age = 30 days  

📸 **Screenshot:**  
![Image](https://github.com/user-attachments/assets/0df5ef38-21d0-43cb-baa3-c5d3d5c907e7)

![Image](https://github.com/user-attachments/assets/7e10fba4-cf54-4935-91a7-28faa8050e75)

![Image](https://github.com/user-attachments/assets/f52c39a4-4433-429f-84ae-d5eeb6b1ba19)

![Image](https://github.com/user-attachments/assets/6f91ae5a-295a-4e2a-8b40-8830b2ab5f55)

![Image](https://github.com/user-attachments/assets/423532f7-30d4-4759-94b8-eac812f9f32f)

---

## 🔐 Step 5: Password Reset & Account Unlock

1. Right-click user → *Reset Password*.  
2. Set a new temporary password.  
3. Enabled account if locked.

📸 **Screenshot:**  
![Image](https://github.com/user-attachments/assets/3a5e9e0f-abb9-4a4e-adb3-44281bea95ea)

![Image](https://github.com/user-attachments/assets/cafa4557-9a0c-494d-869f-94bac45c64a9)

---

## 🗂 Step 6: Shared Folder and Permissions

1. Created a shared folder `D:\Shared`.  
2. Granted access to `Helpdesk` group with read/write permissions.  
3. Verified access from Windows 10 client.

📸 **Screenshot:**  
![Image](https://github.com/user-attachments/assets/5ac15ca7-e57d-4e0f-945f-710ee54d455b)


![Image](https://github.com/user-attachments/assets/95703d93-9a07-4d0f-bd8b-179d1734fdec)

![Image](https://github.com/user-attachments/assets/74bdaf52-901f-493d-9598-c5b025cb96cf)

![Image](https://github.com/user-attachments/assets/f7632b60-66b1-4937-ac10-fee633ce9b9f)

---

## 🖥 Step 7: Join Windows 10 Client to Domain

1. Changed **Computer Name → Domain: purekarlab.local**.  
2. Rebooted and logged in using domain credentials.

📸 **Screenshot:**  
`/screenshots/07_client_domain_join.png`

---

## 🧰 Step 8: Troubleshooting Scenarios

| Scenario | Action Taken | Result |
|-----------|--------------|--------|
| Forgot password | Reset via ADUC | Success |
| Shared folder access denied | Adjusted NTFS permissions | Success |
| DNS not resolving | Flushed DNS and restarted service | Success |

📸 **Screenshot:**  
`/screenshots/08_troubleshooting.png`

---

## 💾 Commands Used (PowerShell Examples)

```powershell
# Reset user password
Set-ADAccountPassword -Identity "helpdesk.user" -NewPassword (ConvertTo-SecureString "New@1234" -AsPlainText -Force)

# Unlock account
Unlock-ADAccount -Identity "helpdesk.user"

# Show domain users
Get-ADUser -Filter * | Select-Object Name, Enabled
