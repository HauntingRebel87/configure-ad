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
  <img width="2447" height="1175" alt="image" src="https://github.com/user-attachments/assets/0182507b-5562-42b4-8879-91bbac2d946f" />
 
</p>

<p>
  Create your resource group and name is Active-Directory.
</p>

<p>
  <img width="1956" height="794" alt="image" src="https://github.com/user-attachments/assets/73fe29d0-9fa3-4e4f-bd85-801c58f3fd3d" />
</p>

<p>
  Go to Virtual Machine and create a new VM. This time your Resource group will be Active Directory. Your VM name will be Active-Directory-VNet. Make sure you set your region to the same as your Active Directory.
</p>
<p>
<img width="870" height="678" alt="image" src="https://github.com/user-attachments/assets/32363d1d-492a-4849-abd6-5a814bbdfe25" />

</p>
<p>
Go to back toVirtual Machine. Create your first VM naming it Domain Controller, or DC-1 to shorten it up. Add it to Active-Directory resource group. Make sure to keep your region the same as your Active Directoy and your VNet. Use Windows Server 2022, size should be standard with 2 vcpus. Set your user name and password, then hit create.

  <p>
    <img width="894" height="792" alt="image" src="https://github.com/user-attachments/assets/f1295169-192b-405c-8190-dc93fb8d3aaf" />

  </p>
  Create another VM naming it Client-1, ensuring it is in the same Resource group as your first VM using Windows 10 and click create.
  Set your DC-1 VM address from dynamic to static. To do this go to Network > Network Interface > IP Configure and set it from there.
  Ensure both VM's are running.
   In your remote desktop log in as DC-1 with the IP address.
  
</p>
<p>
  <img width="1762" height="929" alt="image" src="https://github.com/user-attachments/assets/a8f7add4-9bb2-43b5-915f-cd4c22d5b365" />

</p>

<p>
  Once you have logged in, search run and type in WF.MSC.
</p>

<p>
  <img width="2039" height="1513" alt="image" src="https://github.com/user-attachments/assets/611591f2-0b9d-4724-ab47-21ee62267387" />

</p>

<p>
  From here you will need to disable to Firewall. To do so, click on Firewall properties, click the drop down menu and turn to off. Clip apply and then okay. And log out.
  Go back to your Virtual machine, go into DC-1 to get the Private IP address and copy.
  Go back to your VM and click on Client-1. Go to Network Settings > Network Interface > DNS Servers > Custom and then paste DC-1 IP address. Hit apply afterwards to update your changes.
  Go back to Virtual Machines. Click the box next to your Client-1 and hit refresh. This will make sure that the IP address was changed.
  In Client-1 go and copy the public IP address.
  Go to your Remote Desktop and log in as Client-1. We are going to attempt to ping DC-1's private IP address.
  Back to your VM, click on DC-1 and copy the private IP address.
  Go back to Client-1 in your remote desktop. Open up PowerShell.
</p>

<p>
  <img width="3441" height="1632" alt="image" src="https://github.com/user-attachments/assets/a8ddd231-1137-475e-bd5d-edbd16e49e4a" />

</p>

<p>
  It should look like this, which means you have successfully pinged DC-1. If you get a message that says destination host unreachable, it could just mean that the Firewall is still on, which means it is being blocked. Or the IP address' are in different networks.
</p>
<br />

