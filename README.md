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
  <img width="1789" alt="Screenshot 2023-07-06 at 4 10 47 PM" src="https://github.com/Johnremilekun/configure-activedirectory/assets/30168186/a1785795-76d3-48a8-ae7c-43c9433cae90" height="80%" width="80%" alt="Step 1-1"/>
</p>
