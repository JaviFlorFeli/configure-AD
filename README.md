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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>
The first step is to head over to https://portal.azure.com where you will create two virtual machines.
The first VM you will make is going to be named DC-1, this will be used as the Domain Controller. You will use Windows Server 2022, it is recommended to select a size option of atleast 2 cpus, you are welcome to use more. While creating the VM in the "Resource Group" box, select "create new" and type in "AD-Lab".
<p>
<img src="https://imgur.com/c8dMDFa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

After creating the DC-1 VM
  - Go to the "Virtual Machines" page in Azure 
  - Click on the "DC-1" VM
  - On the left side of the page, in the "Networking" section. Click on the "Network Settings" 
  - Near the top you will see a blue highlighted section with the title of "Network Interface" click on the blue.


<img src="https://imgur.com/ig8v8GZ.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

You will notice in the Private IP Addres section that the Ip address is (Dynamic), we want to change that to be (Static) to ensure that the IP address won't change.
You will do that by clicking on the blue highlighted option that says "ipconfig1"

<img src="https://imgur.com/4duUtEJ.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

You will see a small page pop up on the right side of your screen. 
In the "Allocation" section you want to select the "Static" option and click "save" at the bottom.

<img src="https://imgur.com/n1a9wSU.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

The next step is to create another VM, this one will be named "Client-1". It will be used as the client VM. You will use Windows 10 pro. It is also recommended that this VM is created with the size of atleast 2 cpu's. While creating the VM be sure to go to the Resource Group section and select "AD-Lab". The same one that was created on the DC-1 VM. In the top tabs you will see "Networking". Go to the page, in the Virtual Networks section select the "DC-1-vnet" as we want both of these VM's running in the same virtual network for this lab.

<img src="https://imgur.com/fwX7QoK.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>



<img src="https://imgur.com/Youf12Z.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
