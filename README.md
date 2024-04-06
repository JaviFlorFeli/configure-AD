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

Log back in to DC-1 and in the menu type "Active Directory Users and Computers".

<img src="https://imgur.com/k7jn3ZD.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

On the left hand side, depending what you named your domain. You will see "mydomain.com"
  - Right click the tab
  - Select "New"
  - Select "Organizational Unit"

<img src="https://imgur.com/OtuqJcv.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

You will create two Organizational Units
  - _EMPLOYEES
  - _ADMINS

<img src="https://imgur.com/vJbHfEA.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/L75ndoc.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Once made click on the _ADMINS tab and in the big empty space you will right click. Select "NEW" then select "user".

<img src="https://imgur.com/kjhDouy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Fill in the information accordinglly

When you get to the password page
  - Make sure that the change password box is no longer checked.
  - Check the password never expires box
  - create the user

<img src="https://imgur.com/K7hwISA.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/PCJ5018.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

You have now created your first user. Although he is in the _ADMINS tab, that holds no meaning. We still have to promote him to be an admin. Right click on his name and go to the "Properties" option

<img src="https://imgur.com/GfKh4Nn.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

When looking at the User's properties:
  - go to the "Member of" tab
  - Click on "Add"
  - Type "domain" select check names. Click on "Domain admins"
  - Select "OK"
  - Select "Apply", then "OK"

<img src="https://imgur.com/3vDUsii.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

That user is now an admin. When logging on to the DC-1 as an admin, you will fill in the username similar to the one below.

<img src="https://imgur.com/kclrRWG.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

We are now going to join Client-1 to the domain.

First step is to go to the Azure portal, then go to the DC-1 page
  - Get DC-1's private IP address

<img src="https://imgur.com/mNDkv6i.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Now in the Azure Portal, go to Client-1's page
  - Got to Network Settings
  - Click on "Network Interface"

<img src="https://imgur.com/Bd0Fh5e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

  - Click on DNS Servers
  - Select "Custom"
  - Paste DC-1's private IP below (ensure there are no spaces either before or after the IP)
  - Click "Save"
  - Go back to Client-1's Page and select "restart"
  - Let it completely restart before logging back on

<img src="https://imgur.com/nKIJtGR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/wZTvVSl.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Once restarted, log back on
  - Right click the start menu
  - Select "system"
  - On the right, select "Rename this PC"

<img src="https://imgur.com/W7TRtoD.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

  - Click "Change"
  - Select "Domain". Type in "mydomain.com"
  - Select "Ok", "Apply", and "Ok"

<img src="https://imgur.com/QkP9Cyh.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

You will then see this screen pop up. Fill in the user/Pw with the admin account that was made.

You will see a pop up that says "Welcome to the mydomain.com Domain". After you select ok you will get a few more questions and the computer will ask you to restart. Make the computer restart.

<img src="https://imgur.com/b03Vb8f.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

<img src="https://imgur.com/xKRAk9h.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

When logging back on to Client-1. Now you will sign in with the Admin credentials that you made.

<img src="https://imgur.com/rzvOWLE.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

  - Right click start menu and select "System"
  - On the right click on "Remote Desktop"
  - click on "Select users that can remotely access this pc"
  - Click "Add"
  - Type in "Domain Users"
  - Click "Check Names"
  - Click "Ok"

<img src="https://imgur.com/YDrgR3s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://imgur.com/QQtQiAz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

The next step is to create a bunch of additional users. Then attempt to login with one of the many users created.
  - Go over to DC-1, should still be opened. If not, log back in using the admin account made.
  - Below in the menu, search for "Powershell ISE"
  - Before opening, right click on power sheel and select "Run as Administrator"

<img src="https://imgur.com/DcNeixI.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

Using this link (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
  - Copy the file
  - In powershell, open a new script
  - Paste the file into the new script
  - Run the script
  - You will see 10,000 random users being generated

<img src="https://imgur.com/dUVSEGd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/K8r1OU9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Going back to "Active Directory Users and Computers"
  - Go to "_EMPLOYEES"
  - Double click on any of the random users generated"
  - You will their properties go to the "Account" tab
  - Copy the user logon name


<img src="https://imgur.com/KbpIwCH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Go back to the Client-1 VM and logout of the current account

Sign back in to the VM 
  - type in "mydomain.com\" then paste the name of the random user.
  - All users were generated to use the password "Password1"
  - Attempt to login

<img src="https://imgur.com/S9BiPdn.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

If you see this screen you have successfully logged in to the random generated user's account on the Client-1 VM.

<img src="https://imgur.com/TdmVSm7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
