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


### Step 3 - Creating Organizational Units (OU), Group Policy Object (GPO)

In this section, we will be creating OUs for different department (e.g. Sales, HR), create user accounts and groups with the OUs.
Here i created OUs (Africa, Europe, Asia) with Groups (HR, Sales) under the OUs and users (Tom Hardy, Uncle Hugo) under the group as shown below.

<img width="446" alt="image" src="https://github.com/user-attachments/assets/a1903bf7-d804-4d5c-8264-652a2c083509" />

A GPO is a virtual collection of policy settings, security permissions, and scope of management (SOM) that you can apply to users and computers in Active Directory.
Policy settings are divided into policy settings that affect a computer and policy settings that affect a user. Computer-related policies specify system behavior, application settings, security settings, assigned applications, and computer startup and shutdown scripts. User-related policies specify system behavior, application settings, security settings, assigned and published applications, user logon and logoff scripts, and folder redirection. Computer settings override user-related settings.

![GPO](https://github.com/user-attachments/assets/921121b3-d7d8-4bc5-9080-c8c6cc1715b3)

In this section, we will be setting policies for Password reset policy after 90 days, Wallpaper, Account lock policy.

1. In the Group Policy Management right click on the domain (masterkit.com) to create a GPO (Password reset after 90 days) in the domain.

![GPO](https://github.com/user-attachments/assets/d1603c6b-d360-47b4-ac62-7d09ac7a5bb4)

![GPO set](https://github.com/user-attachments/assets/befabe55-f887-47b4-9918-ce89abb0bb73)

In this photo below we were able to set a password policy for Min and Max password age and also complexity.

![Others](https://github.com/user-attachments/assets/ec4e17d6-ac61-43ab-bc70-b8814ac54f6e)

2. For the next GPO which is for the (Wallpaper), follow same process and name policy as Wallpaer.

![wallaper](https://github.com/user-attachments/assets/b0bc7ac3-3d7c-4e29-b7a8-429c50843174)

![afterWallpaper](https://github.com/user-attachments/assets/89a4432c-ccb1-4c35-8433-162f84278687)

The picture before shows the Desktop Wallper before the Policy Application and after.

![beforewallaper](https://github.com/user-attachments/assets/6114fad4-d9b5-4c90-aa5a-671a0c8cb7c7)

<img width="845" alt="image" src="https://github.com/user-attachments/assets/8d2fda16-fa1d-412c-aa2b-abbc838760dd" />

3. The last example, we will be creating a GPO for "Account Lock Policy". This policy helps prevent brute force attack on user accounts. Here, if 4 wrong logon attempts are been made the accounts automatically locks out.

<img width="835" alt="image" src="https://github.com/user-attachments/assets/fecc4b78-a381-4bf9-a1da-445d93e1ddc4" />

<img width="646" alt="image" src="https://github.com/user-attachments/assets/7baa2249-5e59-44f5-a706-1847c279d994" />


## JOINING CLIENT COMPUTER TO DOMAIN
In this section i will be joining the Windows 10 client machine to the domain.
Here, i will be configuring the domain controller's IP to static IP and also change the DNS servers to loopback and google DNS.

I was able to set the DC (Domain Controller) with its static IPs and DNS servers

<img width="846" alt="image" src="https://github.com/user-attachments/assets/af5b442b-4fa1-48b3-8714-29f1613224e2" />

<img width="716" alt="image" src="https://github.com/user-attachments/assets/2a2ae93a-a2a2-4944-8ad6-2434045f2646" />

In the Client Machine (USER1) i was able to setup the DNS server to resolve to the DC IP

<img width="789" alt="image" src="https://github.com/user-attachments/assets/dacae0c6-7c26-4764-b602-7a67cfe4e73e" />

Also i was able to ping the DC IP which was successful

![image](https://github.com/user-attachments/assets/590cbe1b-365a-4661-a508-4e32fe36828d)

The below picture involves setting the client machine's name (USER1) and adding the (masterkit.com) domain name.

![image](https://github.com/user-attachments/assets/be9c0d06-2859-49b1-89a9-cf9d0e39589e)

After setting up the client machine's name and domain we get this notification for a successful addition.

<img width="254" alt="image" src="https://github.com/user-attachments/assets/29aadc93-4aec-4d68-8463-b2e785a8f43b" />

<img width="262" alt="image" src="https://github.com/user-attachments/assets/de3dfc5f-6c33-4288-b5d3-de512b52c9d1" />
































































