# Active Directory Lab

## Objective
[Brief Objective - Remove this afterwards]

The objective of this project was to design and secure a simulated enterprise Active Directory environment while implementing identity and access management best practices. This lab focused on enforcing least-privilege access through role-based security groups and automating account lifecycle tasks using PowerShell to improve administrative efficiency and reduce security risk. The goal was to replicate real-world cybersecurity and IT operations workflows in a controlled virtual environment.

### Skills Learned
[Bullet Points - Remove this afterwards]

**Active Directory Administration** – Created and managed users, groups, and Organizational Units within a Windows Server domain environment.

**Identity & Access Management (IAM)** – Implemented role-based access control (RBAC) using security groups to enforce least-privilege principles.

**PowerShell Automation** – Automated user provisioning, password resets, account unlocks, and group assignments using AD cmdlets.

**Account Lifecycle Management** – Managed account creation, modification, and remediation processes in alignment with security best practices.

**Access Control & Privilege Management** – Reduced overprivileged access by assigning permissions through structured group-based models.

**Security-Oriented Lab Design** – Built a virtualized enterprise environment to simulate real-world IT and cybersecurity operations.

### Tools Used
[Bullet Points - Remove this afterwards]
-Windows 11 
-Windows 22 Server
-Oracle VB

## Steps

### 1.Setting Up Server as Domain Controller

-Installed Active Directory Domain Services (AD DS) role.

-Promoted the server to a Domain Controller (xyz.local).

-Configured DNS automatically during promotion.

-Verified domain functionality post-restart.

### 2. Domain Users and Group Structure 

Created Organizational Units to simulate departments:

Engineering

Management

IT

Implemented role-based security groups (e.g., Engineering Share).

Created domain users and assigned them to appropriate security groups.

Designed OU structure to reflect enterprise organizational hierarchy and enforce administrative boundaries.

### 3. Attaching Windows 11 Client to Domain
#### Network Details
- Within the server I went to Tools/Network/NAT Network and renamed the network to ADnetwork for easier identification

  Below are the network details

<img src="Documentation/Screenshots/Screenshot%202026-02-28%20160558.png" width="600" height="300">

#### Configuring Static IP Adress

-Set up a static IP adress for both the Windows server and client by onfiguring the network adapter settings to match the IP configuration identified via ipconfig.
-Same configuration was then repeated on the Windows 11 client

Static addressing prevents domain authentication failures caused by dynamic IP changes.

#### Attaching to the Domain

-In the settings for the client I went to Access work or school/Join this device to a local active directory domain/enter domain name/enter username and password/restart the computer
-To confirm the client was attached to the domain I went to Active Direcetory Users and Computer and confirmed the computer(WS01) was listed






















drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*
