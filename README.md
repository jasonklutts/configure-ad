<p align="center">
<img width="307" height="171" alt="image" src="https://github.com/user-attachments/assets/c71d2b7f-fd0b-4131-a753-7ba5704c7d0a" />
</p>

# Microsoft Active Directory Deployed in the Cloud with Microsoft Azure

This tutorial outlines the implementation of **Microsoft Active Directory** with **Microsoft Azure Virtual Machines**.

---

## Environments and Technologies Used
- Microsoft Azure (Virtual Machines)  
- Remote Desktop Connection  
- Microsoft Active Directory Domain Services  
- PowerShell ISE  

---

## Operating Systems Used
- **Domain Controller (DC-1):** Windows Server 2022  
- **Client-1:** Windows 10 Pro  

---

## High-Level Deployment and Configuration Steps
1. Install Active Directory on **DC-1**  
2. Create a **Domain Admin User**  
3. Join **Client-1** to the domain (`mydomain.com`)  
4. Enable **Remote Desktop** for non-admin users  
5. Create additional **non-admin users** with PowerShell  

---

## Deployment and Configuration Steps

### Step 1 — Install Active Directory
On **DC-1**:  
- Open **Server Manager** → **Add Roles and Features**  
- Install **Active Directory Domain Services (ADDS)**  
- Select **Rename this PC (advanced)** → promote to Domain Controller  
- Setup a new forest: `mydomain.com`  
- Restart DC-1 and log in as: mydomain.com\labuser

<img width="738" height="403" alt="image" src="https://github.com/user-attachments/assets/0a00cac6-ae1d-499d-b201-1b49b6f1e138" />
<img width="700" height="504" alt="image" src="https://github.com/user-attachments/assets/712250cc-783e-4ae0-bb3e-191ae1a12ed9" />
<img width="742" height="575" alt="image" src="https://github.com/user-attachments/assets/c1e2766a-e22b-4f01-a0a6-853b619140c9" />


---

### Step 2 — Create a Domain Admin User
In **Active Directory Users and Computers (ADUC)**:  
- Create two Organizational Units (OUs): `_EMPLOYEES` and `_ADMINS`  
- Create a user: **Jane Doe** → `jane_admin`  
- Add `jane_admin` to the **Domain Admins** Security Group  
- Log back into DC-1 as:  mydomain.com\jane_admin

<img width="592" height="401" alt="image" src="https://github.com/user-attachments/assets/7f2e65c0-6b4f-48fd-889d-1e6398f8c41c" />

  
![Create Domain Admin User](https://github.com/your-username/your-repo/assets/create-admin.png)
<img width="360" height="474" alt="image" src="https://github.com/user-attachments/assets/d3f465bf-3534-4af6-ae10-1f52152accf7" />

---

### Step 3 — Join Client-1 to the Domain
On **Client-1**:  
- Login as local admin  
- Join the VM to the domain `mydomain.com` (system restarts)  

On **DC-1**:  
- Open **ADUC** → verify Client-1 appears  
- Create OU `_CLIENTS` → move Client-1 into it  

<img width="741" height="431" alt="image" src="https://github.com/user-attachments/assets/25094944-b649-4638-b9eb-ee2da263d69f" />
<img width="739" height="429" alt="image" src="https://github.com/user-attachments/assets/53adc271-a90e-4176-a406-da45bba43be2" />



---

### Step 4 — Enable Remote Desktop for Domain Users
On **Client-1** (logged in as `jane_admin`):  
- Open **System** → **Remote Desktop**  
- Select **Users that can remotely access this PC** → add **Domain Users**  
- Now any domain user can RDP into Client-1  

> In production, this would be handled with **Group Policy**.  

<img width="740" height="574" alt="image" src="https://github.com/user-attachments/assets/69ddffc6-038e-4fe5-933d-b7171bad471e" />


---

### Step 5 — Create Non-Admin Users with PowerShell
On **DC-1**:  
- Login as Domain Admin  
- Open **PowerShell ISE (Run as Administrator)**  
- Paste and run the script to bulk-create users  
- Verify accounts in ADUC under `_EMPLOYEES`  

<img width="737" height="458" alt="image" src="https://github.com/user-attachments/assets/cedfbec9-790d-420e-a6ae-92d0300f0e4d" />

---

### Step 6 — Verify New Users
- Open **ADUC** → `_EMPLOYEES` OU shows the new accounts  
- Log into **Client-1** using one of the new accounts  
- Confirm domain login works successfully  

<img width="742" height="433" alt="image" src="https://github.com/user-attachments/assets/ff1dd5f1-46e8-42df-a5f9-891132e0e934" />

---

✅ **Microsoft Active Directory has been successfully deployed in the cloud using Microsoft Azure!**


