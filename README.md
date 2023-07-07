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

Step 1 - Create a virtual machine in Azure 

Set up resources in Azure:
- Create a domain controller VM named "DC-1" using Windows Server 2022, noting the associated resource group and virtual network (VNet).
- Configure the domain controller's NIC with a static private IP address.
- Create a client VM named "Client-1":
- Use the same resource group and VNet from Step 1.
- Ensure both VMs are in the same VNet (verify with Network Watcher).


<p align="center">
<img width="1000" alt="Screenshot 2023-07-06 at 4 10 47 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/a1785795-76d3-48a8-ae7c-43c9433cae90" height="80%" width="80%" alt="Step 1-1"/>
  
<img width="1904" alt="Screenshot 2023-07-06 at 4 14 41 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/e1967498-bba6-4757-9ccc-88a10eccd66d">
  
<img width="1909" alt="Screenshot 2023-07-06 at 4 18 13 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/16fca467-32db-4c10-9cdb-fe258eeb72c3">

<img width="1010" alt="Screenshot 2023-07-06 at 4 30 25 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/2d4eb255-443c-47c4-a423-4238cc065f4e">

<img width="882" alt="Screenshot 2023-07-06 at 4 35 02 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/b1a8a44e-f98b-45d1-87c8-760befc62229">

<img width="999" alt="Screenshot 2023-07-06 at 4 35 54 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/fa69c7ce-4b5e-45a9-9c89-5d8ebd43889f">

<img width="980" alt="Screenshot 2023-07-06 at 4 42 04 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/ec275f3e-8372-4f7d-8afe-d0f51b32973e">

<img width="1305" alt="Screenshot 2023-07-06 at 4 50 51 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/dba81e06-12f3-4a6d-adfb-5cd4db71a860">

<img width="1413" alt="Screenshot 2023-07-06 at 4 51 44 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/2bd4331a-c1ba-4f5b-93dc-eb96d7da6d65">

<img width="1412" alt="Screenshot 2023-07-06 at 4 52 44 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/29e4a361-c2cb-40e8-9151-3b1918c8a3e9">

<img width="1414" alt="Screenshot 2023-07-06 at 4 53 41 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/81ee248d-dc2c-4571-b85d-a9882740399f">

<img width="1417" alt="Screenshot 2023-07-06 at 4 54 31 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/f7856101-a8a3-4b7f-90ef-825bd3f44ce6">





























