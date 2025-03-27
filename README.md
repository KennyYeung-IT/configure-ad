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

![image](https://github.com/user-attachments/assets/3a34d94d-24ed-4670-bab1-cae5d4d79299)
![image](https://github.com/user-attachments/assets/138a2483-853f-44b3-9a0e-7c647e9d388c)
![image](https://github.com/user-attachments/assets/c2321b41-dafe-4f3f-8dbe-8d7a51ed8b50)

<p>
Create two virtual machines: one running Windows 10 and the other running Windows Server DC-1 (Domain Controller-1). Both virtual machines will operate on the same virtual network. The domain controller's IP address will be changed from dynamic to static.
</p>
<br />

![image](https://github.com/user-attachments/assets/1e336f19-234a-4651-b627-b25757a8f6d7)

<p>
next, we will disable the firefall on public and private profiles by running "wf.msc"
</p>
<br />

![image](https://github.com/user-attachments/assets/8e55cff9-a0b9-4451-9b85-946bbefc1e41)
![image](https://github.com/user-attachments/assets/a86d6d03-74bc-48a9-a2d8-0d6384c9a2a5)

<p>
After disabling the firewall, we'll update the DNS server on the Windows 10 virtual machine to DC-1's private IP address through the Azure Portal. Navigate to Virtual Machines, then Network Settings, and select DNS Servers.
</p>
<br />

![image](https://github.com/user-attachments/assets/702cb65f-f9f5-4916-b164-598842365577)
![image](https://github.com/user-attachments/assets/31ab10ba-144a-49ca-973b-cb95237f426d)

<p>
RDP back into DC-1 and install Active Directory Domain Services through service manager. Create a new forest "mydomain.com" and promote DC-1 as the domain controller.
</p>
<br />


![image](https://github.com/user-attachments/assets/dda0ee16-a3d4-479d-a6ba-d8046b346e45)
![image](https://github.com/user-attachments/assets/c9d85629-99b1-494f-9a6c-e49d36cf8b28)

<p>
In DC-1 create 3 organizational units named _EMPLOYEE, _ADMIN, and _CLIENT through Windows Administrative Tools and Active Directory Users and Computers (ADUC). Then create a new user "jane doe" and promoter the user to th Domain Admins security group. 
</p>

![image](https://github.com/user-attachments/assets/c1e842fd-5470-4d6b-83b1-529e161a9ab3)
![image](https://github.com/user-attachments/assets/4b353840-b909-43c9-8740-fd5b7ba9d93f)


<p>
To join the Windows 10 virtual machine to the domain, RDP into the system and go to its settings. In the 'Rename this PC (Advanced)' section, change the domain to mydomain.com.

</p>
<br />

![image](https://github.com/user-attachments/assets/291ec94c-3cfe-4b1f-a78f-c495f279fb08)
![image](https://github.com/user-attachments/assets/10007c0e-bb3e-4b81-a2f3-29b0da13b26b)



<p>
Although Remote Desktop is accessible to the admin Jane Doe (jane_admin), domain users need to be granted access manually. To do this, go to Settings, navigate to Remote Desktop, and add domain users to allow remote access to the virtual machine.

</p>
<br />

![image](https://github.com/user-attachments/assets/0326a146-3513-4df3-baba-07e334de6aa8)

<p>
"Now that the Windows 10 virtual machine allows domain users, we can create new accounts. Log in as the admin 'jane_admin' on DC-1, then open PowerShell ISE as an administrator. Create a new file, paste the script from  thishttps://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1 , and execute it." Once completed, check ADUC to ensure new users were created in the _EMPLOYEE OU.

</p>
<br />

![image](https://github.com/user-attachments/assets/22f8dff6-5aad-42dc-9a52-948745d2bdc9)

<p>
Lastly, attempt to log in to the Window 10 virtual machine using one of the users generated previously to ensure the users account work. 
</p>
<br />













<br /># configure-ad
