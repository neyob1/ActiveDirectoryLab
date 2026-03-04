
## 🌐 Network Overview

Domain Name: lab.local  
Domain Controller: Windows Server 2022  
Client Machine: Windows 11  

(Add network diagram screenshot here if you create one)


## 🔐 Features Implemented

- Active Directory Domain Services Installation
- Domain Controller Promotion
- Static IP Configuration
- Domain Join (Windows 11)
- Organizational Units (Engineering, IT, Management)
- Security Groups and Group Membership
- NTFS & Share Permissions
- Mapped Network Drives
- Group Policy Objects (Wallpaper Enforcement)
- Account Lockout Policy
- PowerShell User Creation
- Manual & Automated Password Reset

---

## 🧪 Screenshots

### Domain Controller Setup
![DC Setup](Screenshots/01-domain-controller-setup.png)

### OU Structure
![OU Structure](Screenshots/02-ou-structure.png)

### Engineering Share Permissions
![Share Permissions](Screenshots/03-share-permissions.png)

### Group Policy Configuration
![GPO Wallpaper](Screenshots/04-gpo-wallpaper.png)

---

## ⚙️ PowerShell Automation Example

```powershell
Import-Module ActiveDirectory

New-ADUser `
 -Name "John Doe" `
 -GivenName "John" `
 -Surname "Doe" `
 -SamAccountName "jdoe" `
 -AccountPassword (ConvertTo-SecureString "TempPass123!" -AsPlainText -Force) `
 -Enabled $true `
 -Path "OU=Engineering,DC=lab,DC=local"
