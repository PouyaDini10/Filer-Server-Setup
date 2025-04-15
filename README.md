# 🖧 Network File Shares and Permissions Lab

## 🎯 Objective
To configure and test network file share permissions in a Windows Server environment by creating shared folders with varying access levels, assigning security group permissions through Active Directory, and validating access from a domain-joined client.

---

## 🧰 Lab Environment

- **DC-1**: Domain Controller (Windows Server 2022, domain admin account)
- **Client-1**: Domain-joined client (Windows 10 Pro, standard user)

---

## 📁 Step 1: Create Sample Folders with Permissions

1. On **DC-1**, log in as `mydomain\jane_admin`.
2. On **Client-1**, log in as a normal user.
3. On **DC-1**, create the following folders in `C:\`:
   - `read-access`
   - `write-access`
   - `no-access`
   - `accounting`

4. Share each folder via Properties > Sharing tab. Share with `Domain Users` and `Domain Admins` as needed.

### 🔧 Folder Setup & Permissions

#### 📂 read-access (Group: Domain Users | Permissions: Read)
<img src="https://github.com/user-attachments/assets/0d418d25-873e-4834-b29a-2c7d4b96339f" width="600"/>

#### 📂 write-access (Group: Domain Users | Permissions: Read/Write)
<img src="https://github.com/user-attachments/assets/39e0ba0b-4578-4fae-b1e8-dfc73693bc2a" width="600"/>

#### 📂 no-access (Group: Domain Admins | Permissions: Read/Write)
<img src="https://github.com/user-attachments/assets/bee93a82-80c3-4ff8-95ca-459068bc4b11" width="600"/>

#### 📂 Folder Creation Snapshot
<img src="https://github.com/user-attachments/assets/0876e9df-3d90-4428-8691-80d21bedf09f" width="600"/>

---

## 🧪 Step 2: Test Access from Client-1

5. On **Client-1**, open File Explorer and navigate to `\\dc-1`.

<img src="https://github.com/user-attachments/assets/b7d28e5c-e8b2-430f-aa9e-6368c86340d7" width="600"/>

### 🔍 Access Attempt Results

#### ✅ Read-Access Folder
<img src="https://github.com/user-attachments/assets/01142f6a-9738-464c-89ef-c72df517cb4b" width="600"/>

#### ✅ Write-Access Folder (Created a text file)
<img src="https://github.com/user-attachments/assets/ca55d81c-9461-4baf-ba42-177d211a3fd0" width="600"/>

---

## 👥 Step 3: Create 'ACCOUNTANTS' Group and Assign Permissions

6. On **DC-1**, open **Active Directory Users and Computers (ADUC)** and create a security group named `ACCOUNTANTS`.

<img src="https://github.com/user-attachments/assets/bdf97ce8-981f-48ad-9ba8-71a4b8227814" width="600"/>

7. Set folder permissions:
   - **Folder**: accounting
   - **Group**: ACCOUNTANTS
   - **Permissions**: Read/Write

<img src="https://github.com/user-attachments/assets/5e233c97-57fe-4bf1-aed0-e74ca04f7041" width="600"/>

---

## 🚫 Step 4: Test Access Before Permissions Are Granted

8. On **Client-1**, try accessing the `accounting` folder via `\\dc-1`. Access should be denied.

<img src="https://github.com/user-attachments/assets/d6dc7058-ef0b-48e3-be9b-0c599ccdc330" width="600"/>

---

## ✅ Step 5: Add User to Group and Re-Test

9. Back on **DC-1**, in ADUC, add user `gida.wupa` to the `ACCOUNTANTS` security group.

<img src="/mnt/data/e47d40b5-7040-4a85-8450-a2114c1e2d59.png" width="600"/>

10. On **Client-1**, log in as `gida.wupa` and access the `accounting` folder again.

<img src="/mnt/data/29ad5854-cde5-421e-b797-e09c322438c6.png" width="600"/>

---

## 📌 Summary
- Shared folders were configured with different access levels.
- Active Directory security groups were created and used to manage permissions.
- Access was tested before and after group membership changes.

---

> ✅ This hands-on lab demonstrates understanding of Active Directory, Windows file sharing, and group-based access control. Perfect for system administration and IT support portfolios!
