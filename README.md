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
`/screenshots/04_gpo_policy.png`

---

## 🔐 Step 5: Password Reset & Account Unlock

1. Right-click user → *Reset Password*.  
2. Set a new temporary password.  
3. Enabled account if locked.

📸 **Screenshot:**  
`/screenshots/05_password_reset.png`

---

## 🗂 Step 6: Shared Folder and Permissions

1. Created a shared folder `D:\Shared`.  
2. Granted access to `Helpdesk` group with read/write permissions.  
3. Verified access from Windows 10 client.

📸 **Screenshot:**  
`/screenshots/06_shared_folder.png`

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
