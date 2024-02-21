<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
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

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
1 

- Setting up resources in Azure
- - Create a Windows SERVER named DC-1 (Domain Controller 1).
  - - Username: Labuser / Password: Password1234 (do not forget your password)
  - go to the DC1 folder in Azure and set the NIC Private IP address to static.
  - - Click on Networking -> dc1519(yours should be different) -> IP configurations -> ipconfig1 -> Allocation to Static.

![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/100dd97c-1c6b-413d-8a9b-69e7a4f864a3)

<br>

![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/203f08e1-601b-46bc-810d-176856ca1199)

- - Create the client's virtual machine Windows 10(21H2) named "Client1." Note: Use the same VNET from DC1.
    
![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/55bfd7db-e233-4e4c-941e-418248adda56)

2 Make sure there is a connection between the Client1 and DC1.
- Login to DC1 and enable ICMPv4 on local firewall. type on search bar "(wf.msc)"
- go to Inbound Rules and enable these two ICMPv4 Rules
![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/dfc0e328-b11d-408d-a8ba-5cccea8aa737)

- Login to Client1 with Remote Desktop and ping DC1’s private IP address with "ping -t <private IP address>" on Command Prompt.
![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/ecde4a1a-62fc-4b3d-b9f6-2a3e89343aeb)

3 Install Active Directory
- Server manager should be automatically open on DC1.
- Go to Add Roles and Features and install "Active Directory Domain Services" 
![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/90027fae-a6ff-4877-ae7a-9cd45acd5178)

- add a new forest as "mydomain.com" and click on the Flag -> Promote this server to a domain controller. Choose your password and install it. Note: I chose Password1

![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/914461a7-b857-4604-96b3-78b4195b4566)


![image](https://github.com/cardosoguisilva/configure-ad/assets/157248613/e1f64aab-afa2-4e12-8491-13290209d8d0)

- The Remote desktop will restart automatically, turning the VM into a Domain controller.
- now to log back to VM you will have to add "mydomain.com" in front of your username. Example: mydomain.com\labuser

4 Create an Admin and Normal User Account in Active Directory
- 
