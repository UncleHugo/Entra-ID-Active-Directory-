# Active-Directory Set up

A directory is a hierarchical structure that stores information about objects on a network. A directory service, such as Active Directory Domain Services (AD DS), provides the methods for storing directory data and making this data available to network users and administrators. For example, AD DS stores information about user accounts, such as names, passwords, phone numbers, and so on. AD DS also provides a way for authorized users on the same network to access this information. https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview 

A domain controller is a server running the Active Directory Domain Services (AD DS) role. It authenticates and authorizes all users and computers in a Windows domain-type network, assigning and enforcing security policies for all computers and installing or updating software. For example, when a user logs into a computer which is part of a Windows domain, Active Directory checks the submitted username and password and determines whether the user is a system administrator or a non-admin user.Furthermore, it allows the management and storage of information, provides authentication and authorization mechanisms, and establishes a framework to deploy other related services: Certificate Services, Active Directory Federation Services, Lightweight Directory Services, and Rights Management Services.

In this lab i wil be setting up Active Directory,this basically guides you through the entire process from configuring your domain and users.

### Prerequisites

I set up two virtual machines (VM) in Azure, 
- Windows Server 2019 Datacenter -x64 Gen2 (for the domain controller). This will manage Active Directory.
- Windows 10 (for the client machine). This machine will join the domain.

### Step 1 - Setting up the Virtual Machines (VM)

In the picture below, we were able to validate and create the Windows server 2019 Datacenter VM.

![validationpass1](https://github.com/user-attachments/assets/88fa5806-2a13-4cfe-a134-0ea98142a812)

<img width="856" alt="image" src="https://github.com/user-attachments/assets/6a9b3286-3782-42c7-bae2-d4beb7020d35" />


The picture below shows the validation and creation of the Windows 10 VM

<img width="425" alt="image" src="https://github.com/user-attachments/assets/4577457d-5d31-40af-8d91-edddf0ff12d6" />

<img width="818" alt="image" src="https://github.com/user-attachments/assets/6bd5e535-2b57-44b9-a60b-caf78e5646c7" />


### Step 2 - Installing Active Directory Domain Service (AD DS)

1. Open Server Manager, select Manage > Add Roles and Features
2. Choose Active Directory Domain Service and Install it

![installAD DS](https://github.com/user-attachments/assets/7396561c-ae9e-49b1-aace-e88d20cedc82)

3. Promote the server to a Domain Controller.
   - Create a new forest (e.g. example.local) in this lab i used masterkit.com as my forest.
     ![forest](https://github.com/user-attachments/assets/1cf81cd6-9410-476e-8fec-f00088d59ae3)
   - Set up DNS and Directory Service Restore Mode (DSRM) passowrd.
  
4. Restart the server to apply changes.

<img width="825" alt="image" src="https://github.com/user-attachments/assets/b6464be3-c77c-4dc9-b026-70625646840e" />


### Step 3 - Creating Organizational Units (OU)

In this section, we will be creating OUs for different department (e.g. Sales, HR), create user accounts and groups with the OUs.
Here i created OUs (Africa, Europe, Asia) with Groups (HR, Sales) under the OUs and users (Tom Hardy, Uncle Hugo) under the group as shown below.

<img width="446" alt="image" src="https://github.com/user-attachments/assets/a1903bf7-d804-4d5c-8264-652a2c083509" />




























