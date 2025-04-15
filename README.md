# Network File Shares and Permissions Lab

## Objective
To configure and test network file share permissions in a Windows Server environment by creating shared folders with varying access levels, assigning security group permissions through Active Directory, and validating access from a domain-joined client.

## Environments Used

- DC-1 (Domain admin account on(Server 2022))
- Client-1 (Normal user(Windows 10 Pro))

## Create some sample file shares with various permissions

1. Connect into DC-1 as the domain admin account(mydomain.com\jane_admin).
2. Connect into Client-1 as just a normal user(mydomain.com\{some user}).
3. On DC-1, on the C:\drive, I will create 4 folders: “read-access”, “write-access”, “no-access”, and “accounting”.
4. Open the C: drive, right-click on the specified folder, open properties, click sharing, and share. From there, you can share with anyone you choose over the network. I will be adding the Domain Users and Domain Admins groups. 

### Create our sample folders
![image](https://github.com/user-attachments/assets/0876e9df-3d90-4428-8691-80d21bedf09f)


#### Folder: “read-access”, Group: “Domain Users”, Permissions: “Read”
   
 ![image](https://github.com/user-attachments/assets/0d418d25-873e-4834-b29a-2c7d4b96339f)

#### Folder: “write-access”, Group: “Domain Users”, Permissions: “Read/Write”

   ![image](https://github.com/user-attachments/assets/39e0ba0b-4578-4fae-b1e8-dfc73693bc2a)

#### Folder: “no-access”, Group: “Domain Admins”, Permissions: “Read/Write”

![image](https://github.com/user-attachments/assets/bee93a82-80c3-4ff8-95ca-459068bc4b11)


## Attempting to access file shares as a normal user

5. On Client-1, navigate to the shared folder(In File explorer search for "\\dc-1").
6. From here, I will try to access the folders I just created.

#### File explorer search for "\\dc-1
![image](https://github.com/user-attachments/assets/b7d28e5c-e8b2-430f-aa9e-6368c86340d7)

<br><br>
#### Read-access only

![image](https://github.com/user-attachments/assets/01142f6a-9738-464c-89ef-c72df517cb4b)

#### Read/Write access
As displayed below, I successfully created a text document inside this folder with Read/Write access.

![image](https://github.com/user-attachments/assets/ca55d81c-9461-4baf-ba42-177d211a3fd0)


## Create an ACCOUNTANTS Security Group, assign permissions, and test access

7. In DC-1, in Active Directory Users and Computers(AD UC), I will create a new security group called “ACCOUNTANTS”.
8. On the accounting folder I created earlier, I will set the following permissions:  Folder: “accounting,” Group: “ACCOUNTANTS,” Permissions: “Read/Write.”
9. On Client-1, I will try to access the "accounting" folder. It should fail(we haven't granted permission yet). To access the accounting folder, on File Explorer, search for "\\dc-1".
10. On DC-1 VM, open AD UC(Active Directory Users & Computers), navigate to the Groups OU(Organizational Unit), and under "ACCOUNTANTS, I'm going to add this user "gida.wupa" to the security group.
11. Back on the Client-1 VM, logged on as "gida.wupa" user, I will attempt to open the folder and see if I was granted access.

### Create 'ACCOUNTANTS' Group in AD on DC-1
![image](https://github.com/user-attachments/assets/bdf97ce8-981f-48ad-9ba8-71a4b8227814)

### Set Read/Write Permissions for 'ACCOUNTANTS' on Accounting Folder
![image](https://github.com/user-attachments/assets/5e233c97-57fe-4bf1-aed0-e74ca04f7041)

### Test Access to 'Accounting' Folder from Client-1 (Expect Fail)
![image](https://github.com/user-attachments/assets/d6dc7058-ef0b-48e3-be9b-0c599ccdc330)

### Verify 'ACCOUNTANTS' Folder Access as gida.wupa on Client-1
![image](https://github.com/user-attachments/assets/37944eb4-3e92-4a9e-8d55-99fc572da189)




















