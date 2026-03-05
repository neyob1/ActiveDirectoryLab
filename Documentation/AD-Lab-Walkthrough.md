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

### 2. Creating Domain Users

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

<img width="500" height="400" alt="Network Details" src="https://github.com/user-attachments/assets/d37ed400-e722-46ac-9e21-c9b6aeb6813f" />

#### Configuring Static IP Adress

-Set up a static IP adress for both the Windows server and client by onfiguring the network adapter settings to match the IP configuration identified via ipconfig.
-Same configuration was then repeated on the Windows 11 client

Static addressing prevents domain authentication failures caused by dynamic IP changes.

#### Attaching to the Domain

-In the settings for the client I went to Access work or school/Join this device to a local active directory domain/enter domain name/enter username and password/restart the computer

-To confirm the client was attached to the domain I went to Active Direcetory Users and Computer and confirmed the computer(WS01) was listed

Here we can see that our Windows 11 computer is attached to the domain
<img width="500" height="400" alt="Screenshot 2026-02-28 212015" src="https://github.com/user-attachments/assets/3adf9ab8-a765-47ba-94c7-2923bb1d7ab3" />

### 4. Orginazational Units and Access Control Design

- Created three diffrent Orginazational Units (OUs) reprsenting diffrent departments (Engineering,Management,IT) to reprsent a real work enviornment
- Designed the OU structure to reflect departmental seperation when it comes to administration access
- Created a security group called Engineering Share to grant that specific group access to shared resources
  Added:
- 2 users from the Engineering Department
- 1 user from management(simulating cross-department collaboration)

Here are all the users who are present in Engineering Share

<img width="500" height="400" alt="Screenshot 2026-03-01 123542" src="https://github.com/user-attachments/assets/befe4f31-69d9-4d30-a640-c0172de113c1" />

- Assigned permissions to the shared resource using the Engineering Share security group

Under advanced security settings we can ensure that Engineering Share group (besides administrator) is the only one who recieves said permissions

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/b513b326-ec44-4a9f-884f-c07cfc72b42d" />



This approach of creating orginizational groups and even groups within them allows us to add role-based permissions to an entire group instead of having to modify each user indiviudally promoting efficiency.

### 5. Group Policy Objects

Overview

Group Policy Objects (GPOs) allow administrators to centrally manage system configurations and user environments within an Active Directory domain. Policies can be linked to domains or Organizational Units to enforce standardized settings across groups of users or computers.

#### Policy Configuration

- To simulate centralized management within a corporate environment, a Group Policy Object was created for the Engineering Organizational Unit.

- Created a custom desktop wallpaper to represent a department-specific configuration.

- Stored the wallpaper inside the NETLOGON share, which allows domain-wide access to files used in policy deployment.

<img width="500" height="400" alt="movingwallpaperintoNETLOGON" src="https://github.com/user-attachments/assets/616e9400-0ff6-49ac-b6f4-b89d3f3cb236" />

- Copied the file path and configured the wallpaper setting within the newly created GPO.

#### Policy Deployment

- Linked the GPO to the Engineering OU.

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/fbead06a-af0c-4222-b64b-b7e7b52573c3" />

- Logged into domain accounts belonging to Engineering users.

- Verified that the configured desktop background was automatically applied.

- Users outside the Engineering OU were not affected by the policy, confirming that the GPO was correctly scoped.

### 5. Ticket Processing

For this step I processed a ticket regarding a manager who was satisfied with the background we set in the previous step but wanted to prevent the engineers from having the ability to change the background, he emphasized that he only wanted this to apply to the engineering department.

<img width="500" height="400" alt="Screenshot 2026-03-01 143933" src="https://github.com/user-attachments/assets/e3a07205-3e15-4486-b721-9fa6ba135f5f" />

- Under tools in the domain server I accessed group policy management and located the setting that prevents the changing of the background under the engineering organizational unit

<img width="500" height="400" alt="LockingDesktopWallpaper" src="https://github.com/user-attachments/assets/705f46a1-d0c5-4172-8b13-9e6bd6363a08" />

- To confirm the policy was enforced, I logged in as one of the users from the engineering department. I was completely prhohibited from changing the background which can be seen below

<img width="500" height="400" alt="VirtualBox_Windows for HD_01_03_2026_15_01_46" src="https://github.com/user-attachments/assets/d154671b-e65e-4b2d-a445-1a18bb235f56" />

### 6. Task Automation with Powershell

Objective: Task automation is beneficial because instead of doing tasks manually in AD such as creating users manually like we did earlier in step 2, we can write a script that does all of it for us. For this step I utilized Powershell to create a user and fill all the attributes for that user.

The script I used to create the user can be seen below

<img width="500" height="400" alt="Automating Task w Powershell" src="https://github.com/user-attachments/assets/609051e2-f99b-435b-8330-94382dd5a8c8" />

### 7. Resetting AD Passwords

#### Overview

Account lockout policies are commonly used in enterprise environments to prevent unauthorized access and brute-force login attempts. In this lab, an account lockout threshold was configured through Group Policy to simulate a security control used in real-world Active Directory environments.

After three failed login attempts, the user account becomes locked and requires administrative intervention to regain access.

#### Manual Process

First I took a manual approach to for the password reset by doing it through the domain controller, this method is less efficient but demonstrated what goes on behind the scenes.

- Configured an **Account Lockout Policy** under Group Policy Management which locked users out after 3 incorrect login attempts

<img width="500" height="400" alt="Account Lockout Threshold" src="https://github.com/user-attachments/assets/5f142a17-ab5a-4906-9c0d-170c5aa0c1ac" />

- Switched over to the Windows Client and triggered the lockout using one of the created users

- Reset the user's password through **Active Directory Users and Computers**

<img width="500" height="400" alt="pass reset" src="https://github.com/user-attachments/assets/dac8b6de-c0cd-4afb-981f-e545af45e4e6" />

#### Automated Process

For a more effecient practice I repeated this password reset using Powershell automation. 

##### Powershell Script

<img width="500" height="400" alt="reset password PS" src="https://github.com/user-attachments/assets/6d0ab820-9148-46cf-aeb1-56f4c668fd07" />

PowerShell allows administrators to quickly reset passwords and unlock accounts without navigating the graphical interface.

#### Real World Considerations

Applies to both manual and automated process:

- In a real-world enviornment the user would be notified of the temporary password through a secure form of communication
- The user would then login on thier end using that password where they would then prompted to reset it again using thier own password













  























drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*
