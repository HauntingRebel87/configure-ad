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
  1. **Create 2 Virtual Machines**
</p>

<p>
  Create your resource group and name is Active-Directory.
</p>

<p>
  <img width="1956" height="794" alt="image" src="https://github.com/user-attachments/assets/73fe29d0-9fa3-4e4f-bd85-801c58f3fd3d" />
</p>

<p>
  Go to Virtual Machine and create a new VM.
</p>
<p>
  This time your Resource group will be Active Directory. Your VM name will be Active-Directory-VNet. Make sure you set your region to the same as your Active Directory.
</p>
<p>
<img width="870" height="678" alt="image" src="https://github.com/user-attachments/assets/32363d1d-492a-4849-abd6-5a814bbdfe25" />

</p>
<p>
Go to back to Virtual Machine. 
</p>
<p>
  Create your first VM naming it Domain Controller, or DC-1 to shorten it up.
</p>
 <p>
   Add it to Active-Directory resource group. 
 </p>
 <p></p>
 Add your Active Directoy and your VNet. Use Windows Server 2022, size should be standard with 2 vcpus. Set your user name and password, then hit create.
</p>
  <p>
    <img width="894" height="792" alt="image" src="https://github.com/user-attachments/assets/f1295169-192b-405c-8190-dc93fb8d3aaf" />

  </p>
  <p></p>
  Create another VM naming it Client-1, ensuring it is in the same Resource group as your first VM using Windows 10 and click create.
  </p>
  <pSet your DC-1 VM address from dynamic to static. To do this go to Network > Network Interface > IP Configure and set it from there.
  </p>
  <p>
  Set your DC-1 VM address from dynamic to static. To do this go to Network > Network Interface > IP Configure and set it from there.
    </p>
    <p></p>
      Ensure both VM's are running.
    </p>
    <p></p>
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
  </p>
  <p>
  Go back to your Virtual machine, go into DC-1 to get the Private IP address and copy.
  Go back to your VM and click on Client-1. Go to Network Settings > Network Interface > DNS Servers > Custom and then paste DC-1 IP address. Hit apply afterwards to update your changes.
  </p>
  <p>
  Go back to Virtual Machines. Click the box next to your Client-1 and hit refresh. This will make sure that the IP address was changed.
    </p>
    <p>
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
  <p>
  2. **Installing Active Directory**

  Log in to your DC-1 remote computer, using its' IP address to be able to install Active Directory Services.
  Once logged in, click the start menu, and click on Server Manager.
  Click on Roles. This is where we will add Active Directory.
</p>
<p>
  <img width="1707" height="1542" alt="image" src="https://github.com/user-attachments/assets/85342254-1270-4990-9303-f0da5664eea1" />

</p>
<p>
  Make sure to check mark Active Directory Domain Services and click next until you get to the last screen and hit install.
  Go back to your Service Manager, click on the yellow triangle. We are going to promote DC-1 and add a new forest.
  </p>

  Use mydomain.com, click next and make up a password, uncheck the box, click next until last screen and hit install.
  It will automatically restart the computer. Log back into DC-1 as your domain (mydomain.com/username).
    
  Click on start and go to Active Directory Admin Center under Windows Admin Tools.
  Create an Organizational Unit by right clicking on local, new and then organization.
  Under name we will add _Employees, and save. We will need to make another one for _Admins. Can names the Organization Units how you want, but doing it this way allows us to be able to see these folders easier.
  </p>
  
  <p>
  From here we can start adding Employees/Admin to the folders by clicking on the folder, right clicking, new and user.
  Once you added an employee to admin. You can give them administration right by clicking on their name. Scrolling down to Move to, click add. From here you can add them to domin admin (make sure you add the space, otherwise it will not reconize it) and click apply then okay.
  Log out then log back in as the employee you chose to give Admin rights to.
  </p>
  <p>
  3. **Joining Client-1**
  
</p>
<p>
  Login to Client-1 in your Remote Desktop. This is where we will change the Domain/Computer name.
</p>

<p>
  Right click on start and then settings. Scroll down to advance system setting and click it.
</p>
<p>
  Click on change, then click on Domain. Change this is mydomain.com. Click okay, and then enter the admin's name and password for this step. You will need to restart your Remote Desktop.
</p>

<p>
  4. **Powershell**
</p>

<p>
  Login to Powershell as the Admin that was created.
</p>

<p>
  Right click on start menu, and go to Settings then Remote Desktop. Click user accounts, add your domain user. Click okay. This will allow all users to log on to the account.
</p>

<p>
  Login to DC-1 as the Admin you created.
</p>

<p>
  <img width="2565" height="1712" alt="image" src="https://github.com/user-attachments/assets/554891f5-7954-474d-ac81-d43c5dac62fc" />

</p>

<p>
  Login to PowerShell ISE as Admin and click the arrow down button. This is where you will add a script to be able to add all users.
</p>

<p>
  <img width="3086" height="913" alt="image" src="https://github.com/user-attachments/assets/8b647f49-cf2a-48c5-9d57-5e27526d0ba8" />

</p>

<p>
  The script will create 1,000 new users. Once it is finishing creating the new users, open up Active Directory Users and Computers.
</p>

<p>
  <img width="2452" height="1666" alt="image" src="https://github.com/user-attachments/assets/606a3da2-6ea4-4528-8dcc-97d4d9200a25" />

</p>

<p>
  Once you have clicked on _Employees, you will now see all new users that the script has created.
</p>

<br />

