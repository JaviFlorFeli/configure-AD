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

Next, we are going to ensure connectivty between the two VM's
  -First we will login to the Domain Controller VM (DC-1). Go to the DC-1 VM page in Azure and copy the "Public IP Address". Open the Remote Desktop Connection app on Windows and paste the IP Address and continue to login using the username and password you used when creating the VM.

<img src="https://imgur.com/xGqzqaf.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/sbH52Xn.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Once logged in to DC-1 VM, your screen should look similar to this one below.

<img src="https://imgur.com/vxXAcTC.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Down in the menu of DC-1, type "wf.msc"

<img src="https://imgur.com/xFsuBsN.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Once opened you will be sent this screen
  - on the left hand side of the screen select "inbound rules"
  - you will see a long list of rules, go over to the "protocol" tab and click on it.
  - Go down to the two "Echo Request" rules below under the "ICMPv4" protocol and right click each one to "enable rule"

<img src="https://imgur.com/ggPcQ78.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

You can now minimize the DC-1 VM.
  - Next thing you will do is login to the Client-1 VM following the same procedure you did with DC-1 VM
  - Once logged in to the Client 1 VM, down in the menu type in "Command". You will see and open the Command Prompt application.
  - Once opened we will ping DC-1's private IP with the command "ping -t" (perpetual ping)
  - If you see a constant list of the IP address ping, there is connectivity between the two VM's.


<img src="https://imgur.com/poGxWqh.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>



<img src="https://imgur.com/sFKGAm4.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Log back into the DC-1 VM and select the "Add Roles and Features" in the Server Manager dashboard

<img src="https://imgur.com/8OJMaVI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

You will see this screen pop up, continue to select next until you get to the "server roles" tab.

<img src="https://imgur.com/TPO8DTi.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Check the "Active Directory Domain Services" box, and continue to hit the next button

<img src="https://imgur.com/9AwjwYL.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

You will get to the installation tab and click on the "install" button. 

<img src="https://imgur.com/CYW4wYW.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

After doing so, on the dashboard screen, in the top right corner you will see a flag icon with a yellow exclamation point. click on the icon and you will see a blue highlighted option to promote, which you will click on.

<img src="https://imgur.com/DgOXBVx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Select the "Add a New Forest" option and in the root domain name box. type in "mydomain.com" (or anything else).

<img src="https://imgur.com/nTl8iqO.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

After selecting next, you will be asked to make a password. For the sake of this lab, you can use a simple password such as "password1". Just make sure you do not forget that password. continue to hit next until you have the option to select "install"
  - once you have hit install, it may take a while for the installation. after the install is complete the VM will restart and sign you out automatically. 

<img src="https://imgur.com/Z70hGIs.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Once logged out, log back in to the DC-1 VM.
  - Before copying IP address from Azure refresh the page.
  - Paste the IP address into Remote Desktop Connection
  - When logging in, use the root domain name in your username as it is now a Domain Controller.
  - For Example:
      - Username: mydomain.com\labuserjavi
      - Password:**************

<img src="https://imgur.com/khVGzXj.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
