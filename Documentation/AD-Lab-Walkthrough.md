
# 1.Domain Controller Promotion

## Installing Active Directory Domain Services

1. Opened **Server Manager**
2. Selected **Add Roles and Features**
3. Installed:
   - Active Directory Domain Services (AD DS)
4. Enabled automatic restart

## Promoting to Domain Controller

1. Clicked **Promote this server to a domain controller**
2. Selected **Add a new forest**
3. Entered domain name: `lab.local`
4. Set Directory Services Restore Mode (DSRM) password
5. Completed installation and rebooted

# 2. 

## Installing Active Directory Domain Services

1. Opened **Server Manager**
2. Selected **Add Roles and Features**
3. Installed:
   - Active Directory Domain Services (AD DS)
4. Enabled automatic restart

## Promoting to Domain Controller

1. Clicked **Promote this server to a domain controller**
2. Selected **Add a new forest**
3. Entered domain name: `lab.local`
4. Set Directory Services Restore Mode (DSRM) password
5. Completed installation and rebooted


### Result

Server successfully promoted to Domain Controller.


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
