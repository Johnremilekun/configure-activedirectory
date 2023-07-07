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

















