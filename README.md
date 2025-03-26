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

- Step 1: Create a virtual machine running Windows 10.
- Step 2: Create a virtual machine running Windows server DC-1 (Domain Controller-1).  
- Step 3: Set DC-1's ip address to static and disable it's firewall.
- Step 4: Set Windows 10 virtual machine's DNS setting to DC-1 private IP address.
- Step 5: Ping DC-1's private IP address to ensure connection.

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two virtual machines: one running Windows 10 and the other running Windows Server DC-1 (Domain Controller-1). Both virtual machines will operate on the same virtual network. The domain controller's IP address will be changed from dynamic to static.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
RDP back into DC-1 and install Active Directory Domain Services through service manager. Create a new fores "mydomain.com" and promote DC-1 as the domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In DC-1 create 3 organizational units named _EMPLOYEE, _ADMIN, and _CLIENT through Windows Administrative Tools and Active Directory Users and Computers (ADUC). Then create a new user "jane doe" and promoter the user to th Domain Admins security group. 
</p>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To join the Windows 10 virtual machine to the domain, RDP into the system and go to its settings. In the 'Rename this PC (Advanced)' section, change the domain to mydomain.com.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Although Remote Desktop is accessible to the admin Jane Doe (jane_admin), domain users need to be granted access manually. To do this, go to Settings, navigate to Remote Desktop, and add domain users to allow remote access to the virtual machine.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
"Now that the Windows 10 virtual machine allows domain users, we can create new accounts. Log in as the admin 'jane_admin' on DC-1, then open PowerShell ISE as an administrator. Create a new file, paste the script from  thishttps://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1 , and execute it." Once completed, check ADUC to ensure new users were created in the _EMPLOYEE OU.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, attempt to log in to the Window 10 virtual machine using one of the users generated previously to ensure the users account work. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />











<br /># configure-ad
