<p align="center">
<img src="https://i.imgur.com/R5OzmdT.png" height="55%" width="55%" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Microsoft Azure - Active Directory (AD)</h1>

This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
<h2>High-Level Deployment and Configuration Steps</h2>


Set up Azure resources: 

- Create a Windows Server 2022 VM named "DC-1" as the domain controller, noting the resource group and VNet.
- Create a Windows 10 VM named "Client-1" in the same resource group and VNet 

Ensure network connectivity between both VM’s

- Login to "Client-1" via Remote Desktop and continuously ping the private IP address of "DC-1" using the command "ping -t <IP address>".
- On the domain controller, enable ICMPv4 in the local Windows Firewall, and check for a successful ping response from "Client-1".
- Install Active Directory
- Login to DC-1 and install Active Directory Domain Services
- Create an Admin and Normal User Account in AD
- Link the client VM to a domain and log in using the original admin account.
- Configure Remote Desktop for non-admin users on the client VM 
- create additional users, and test logging in with those newly created accounts.

<h2>Step Process</h2>

<h3>&#9312; Create a Domain Controller VM</h3>

A - Create a virtual machine in Azure 

Set up resources in Azure:
- Create a domain controller VM named "DC-1" using Windows Server 2022, noting the associated resource group and virtual network (VNet).
- Configure the domain controller's NIC with a static private IP address.
- Create a client VM named "Client-1":
- Use the same resource group and VNet from Step 1.
- Ensure both VMs are in the same VNet (verify with Network Watcher).


<p align="center">
<img width="1000" alt="Screenshot 2023-07-06 at 4 10 47 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/a1785795-76d3-48a8-ae7c-43c9433cae90" height="80%" width="80%" alt="Step 1-1"/>

<hr>

<img width="1904" alt="Screenshot 2023-07-06 at 4 14 41 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/e1967498-bba6-4757-9ccc-88a10eccd66d">

<hr>

<img width="1909" alt="Screenshot 2023-07-06 at 4 18 13 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/16fca467-32db-4c10-9cdb-fe258eeb72c3">

<hr>

<img width="1010" alt="Screenshot 2023-07-06 at 4 30 25 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/2d4eb255-443c-47c4-a423-4238cc065f4e">

<hr>

<img width="882" alt="Screenshot 2023-07-06 at 4 35 02 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/b1a8a44e-f98b-45d1-87c8-760befc62229">

<hr>

<img width="999" alt="Screenshot 2023-07-06 at 4 35 54 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/fa69c7ce-4b5e-45a9-9c89-5d8ebd43889f">

<hr>

<img width="980" alt="Screenshot 2023-07-06 at 4 42 04 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/ec275f3e-8372-4f7d-8afe-d0f51b32973e">

<hr>

<img width="1305" alt="Screenshot 2023-07-06 at 4 50 51 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/dba81e06-12f3-4a6d-adfb-5cd4db71a860">

<hr>

<img width="1413" alt="Screenshot 2023-07-06 at 4 51 44 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/2bd4331a-c1ba-4f5b-93dc-eb96d7da6d65">

<hr>

<img width="1412" alt="Screenshot 2023-07-06 at 4 52 44 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/29e4a361-c2cb-40e8-9151-3b1918c8a3e9">

<hr>

<img width="1414" alt="Screenshot 2023-07-06 at 4 53 41 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/81ee248d-dc2c-4571-b85d-a9882740399f">

<hr>

<img width="1417" alt="Screenshot 2023-07-06 at 4 54 31 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/f7856101-a8a3-4b7f-90ef-825bd3f44ce6">

<hr>

B 

- Create a client VM named "Client-1":
- Follow the same steps and Use the same resource group and VNet from Step 1.
- Ensure both VMs are in the same VNet.

<hr>

<h3>&#9313; Ensure Connectivity between the Client and Domain Controller</h3>

- Login to both the Domain Controller and Client-01 VMs with Remote Desktop in windows
- This example uses a mac so downlowd Microsoft remote desktop from the app store

<img width="1322" alt="Screenshot 2023-07-06 at 6 07 15 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/ff092c71-600b-41e7-9214-9bcbb6c6d0d4">

<hr>

- Open client-1 VM in Azure, copy the public IP and use it to remote into client one as shown in the screen shot. Do the same with DC-1
- Remote Desktop into "Client-1" and DC-1 


<img width="1219" alt="Screenshot 2023-07-06 at 9 41 02 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/88f75847-ded0-409a-b8d2-e923aa38d198">

<hr>

<img width="988" alt="Screenshot 2023-07-06 at 9 37 23 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/4878a3bf-098f-454d-b209-c90657cb8c6a">

<hr>

- Open windows firewall - advanced settings in client -1
- Click "Inbound Rules" (on the left sidebar). Find the two names "Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In)"
- Select them both, right click then click "Enable Rule"

  

<img width="1013" alt="Screenshot 2023-07-06 at 10 03 57 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/dfdf3418-8f9e-4a97-883d-42521eaa7f78">

<hr>


- Copy private IP from DC-1 then go client - 1 VM
- Open command prompt
- Inside the Command Prompt, type "ping -t {DC-01 Private IP Address}"
- This confirms if the Client VM can see the Domain Controller VM successfully

<hr>

<img width="1106" alt="Screenshot 2023-07-06 at 10 19 19 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/406bab07-86f2-41bb-8d2e-0d419606fe71">


<hr>

<h3>&#9314; Install Active Directory Domain Services within Domain Controller VM</h3>

<hr>


Install active directory on DC.

- Open server manager click on add roles and Follow the insulation process by clicking next and check "Active Directory Domain Services",when you reach server roles Tab

- Setup a new forest as mydomain.com (can be anything, just remember what it is)

- Restart and then log back into DC-1 as user: mydomain.com\labuser

<hr>
<img width="1091" alt="Screenshot 2023-07-07 at 11 06 55 AM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/e0dcef86-b556-48b1-9532-edb98b90e4e4">

<hr>

<img width="1328" alt="Screenshot 2023-07-07 at 11 14 08 AM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/504ee60c-ea2f-47fe-81d4-b06d00be8b23">

<hr>

<img width="1459" alt="Screenshot 2023-07-07 at 11 14 43 AM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/b8bd142e-1d87-42ed-a106-44dfbff0729d">

<hr>

<h3>&#9315; Create an Admin and Normal User Account in AD VM</h3>

<hr>

- On the Domain Controller VM, in Server Manager, click on "Tools" on the top-right header. Click "Active Directory Users and Computers".
- In Active Directory Users and Computers (ADUC), create an "Employees" Organizational Unit (OU) and an "_ADMINS" OU.
- Create a new user account named "Jane Doe" with the username "jane_admin" and the same password.
- Add "jane_admin" to the "Domain Admins" Security Group.
- Logout/close the Remote Desktop connection to "DC-1" and log back in as "mydomain.com\jane_admin".

<hr>

<img width="819" alt="Screenshot 2023-07-10 at 10 53 03 AM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/caa79a07-cb8f-4ec4-8561-4fe6edc7b58e">

<hr>

<img width="1022" alt="Screenshot 2023-07-10 at 11 44 35 AM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/5ea82671-0308-44ad-90fb-277b7f93e75a">


<hr>

<h3>&#9316; join "Client-1" to the domain "mydomain.com" VM</h3>

<hr>

- Configure "Client-1's" DNS settings in the Azure Portal to use the private IP address of the domain controller (DC).
- Restart "Client-1" from the Azure Portal.
- Remote Desktop into "Client-1" as the original local admin (labuser) and join it to the domain (a restart will be required).
- Remote Desktop into the Domain Controller and verify that "Client-1" appears in the "Computers" container within Active Directory Users and Computers (ADUC) at the root of the domain.

<hr>

<img width="1177" alt="Screenshot 2023-07-10 at 11 35 30 AM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/9fb7e11c-0297-4e2b-ab88-cef309c9dd7e">

<hr>

<img width="1462" alt="Screenshot 2023-07-10 at 11 48 23 AM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/8603b36b-dbd3-4f4c-b852-4bf40590d8c6">

<hr>

<h3>&#9317; Setup Remote Desktop for non-administrative users on Client-1 VM</h3>

<hr>

- Log in to "Client-1" as "mydomain.com\jane_admin" and open system properties.
- Click on "Remote Desktop" and allow access for "domain users" to remote desktop.
- Non-administrative users can now log into "Client-1" using Remote Desktop.

<hr>

<img width="1071" alt="Screenshot 2023-07-10 at 12 01 34 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/876a06ce-1a4d-43c7-82e0-abfacc937937">

<hr>

<h3>&#9316; Create additional users and attempt to log into client-1 with one of the users VM</h3>

<hr>

- Log in to "DC-1" as "jane_admin".
- Open PowerShell_ise as an administrator.
- Create a new file and copy the contents of the script from the following link : [script](https://github.com/Johnremilekun/configure-activedirectory/blob/main/script)
- Run the script and observe the user accounts being created.
- Once the script completes, open Active Directory Users and Computers (ADUC) and verify the presence of the accounts in the appropriate Organizational Unit (OU).
- Attempt to log into "Client-1" using one of the created accounts, making a note of the password provided in the script.

<hr>

<img width="1234" alt="Screenshot 2023-07-10 at 5 08 33 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/709ee73d-80eb-4ba4-b1b6-5bb6eba001dd">

<hr>

<h3> DONE </h3>

<hr>


















