# Network File Shares and Permissions Lab

## Objective
This lab demonstrates technical knowledge of **Active Directory (AD)**, focusing on how **file shares** and **permissions** provide security aligned with the **CIA triad**—**Confidentiality, Integrity, and Availability**.  
This is a continuation of the previous lab and requires the virtual machines set up in the first part of the project.

---

## Section 1: File Shares and Permissions Creation

### 1. Connect to the Domain Controller (DC-1)
- Use **Remote Desktop Connection (RDP)** to access `DC-1` using **Domain Admin** credentials.

### 2. Create Shared Folders
- Navigate to the **C:\\ drive**
- Create the following four folders:
  - `read-access`
  - `write-access`
  - `no-access`
  - `accounting`

### 3. Configure Permissions

#### `read-access`
- Right-click > **Properties** > **Sharing** tab > **Share**
- Add **Domain Users**
- Set permission level to **Read**

#### `write-access`
- Add **Domain Users**
- Set permission level to **Read/Write**

#### `no-access`
- Remove **Domain Users**
- Add **Domain Admins**
- Set permission level to **Read/Write**

> ⚠️ Skip configuring the `accounting` folder for now.

---

## Section 2: File Share Access Testing

### 1. Log in to Client-VM
- Use RDP to connect to the **Client-VM** as a **Domain User**

### 2. Access Shared Folders
- Open **File Explorer**
- Enter `\\dc-1` in the address bar to view shared folders

### 3. Test Access Behavior

#### `read-access`
- Attempt to create a file or folder (should be denied)
  - ✅ Demonstrates:
    - **Availability**: Authorized users can view the files
    - **Integrity**: Unauthorized changes are not allowed

#### `write-access`
- Create a `.txt` file (should succeed)
  - ✅ Demonstrates:
    - **Availability & Integrity** for users with write access

#### `no-access`
- Try to open (should be denied)
  - ✅ Demonstrates:
    - **Confidentiality**: Unauthorized access is blocked

---

## Section 3: Creating a Security Group in Active Directory

### 1. Connect to DC-1
- Open **Active Directory Users and Computers**

### 2. Create a New Organizational Unit
- Right-click the domain root > **New** > **Organizational Unit**
- Name it `_groups`

### 3. Create the `ACCOUNTING` Security Group
- Right-click `_groups` > **New** > **Group**
- Name: `ACCOUNTING`

### 4. Set Folder Permissions for `accounting`
- Go to the `accounting` folder on C:\\
- Right-click > **Properties** > **Sharing** tab > **Share**
- Add the `ACCOUNTING` group
- Grant **Read/Write** permissions

---

## Section 4: Testing Security Group Access

### 1. From Client-VM
- As a regular Domain User, attempt to access the `accounting` share (should be denied)
  - ✅ Demonstrates **Confidentiality**

### 2. Add User to the `ACCOUNTING` Group
- On DC-1:
  - Open **ACCOUNTING** group > **Members** tab > **Add**
  - Add the selected Domain User

### 3. Re-test Access
- Log back into **Client-VM** as the same user
- Access the `accounting` share (should now work)
  - ✅ Demonstrates **Availability**

---

## Conclusion
This lab demonstrates how **Active Directory**, file shares, and permission structures enforce the **CIA triad**:

- 🔐 **Confidentiality** – Preventing unauthorized access to sensitive data  
- ✅ **Integrity** – Ensuring only authorized changes are made  
- 📂 **Availability** – Ensuring access for authorized users  

These are foundational principles for maintaining secure and efficient enterprise environments.
