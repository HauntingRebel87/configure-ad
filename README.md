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

- Create 2 Virtual Machines in Azure
- Install Active Directory
- Join Client-1 to Main Domain
- Create a list of User Accounts

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="870" height="678" alt="image" src="https://github.com/user-attachments/assets/32363d1d-492a-4849-abd6-5a814bbdfe25" />

</p>
<p>
Create your first VM naming it Domain Controller, or DC-1 to shorten it up. Use Windows Server 2022, size should be standard with 2 vcpus. Set your user name and password, then hit create.

  <p>
    <img width="894" height="792" alt="image" src="https://github.com/user-attachments/assets/f1295169-192b-405c-8190-dc93fb8d3aaf" />

  </p>
  Create another VM naming it Client-1, ensuring it is in the same network group as you first VM using Windows 10 and click create.
  Set your DC-1 VM address from dynamic to static. To do this go to Network > Network Interface > IP Configure and set it from there.
  Ensure both VM's are running.
  Go to Client-1 in remote desktop and log in. Run command prompt and ping DC-1's private IP address with -t
  
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
