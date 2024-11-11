<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>Configuring Active Directory within Azure VMs</h1>
This tutorial runs through how to set up Active Directory within Azure VMs.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Windows Server 2022 Datacenter: Azure Edition

<h2>Installation Steps</h2>

<p>
<img src="https://i.imgur.com/8bVe0Kl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The first step is to setup a resource group in active directory, this will contain all of the resources used to create the environment we will be creating.
</p>
<br />

<p>
<img src="https://i.imgur.com/YIEeHa4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, setup a virtual network in Azure and just give it the default settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/QhUjx1V.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You will now want to create 2 virtual machines, one to host a client computer running windows 10 and the other running the windows server image. MAKE SURE THEY ARE ON THE SAME VNET. (Log the public and private IP of both VMs)
</p>
<br />

<p>
<img src="https://i.imgur.com/iDvoxmU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
once that is complete connect to the client and the server using RDP.
</p>
<br />

<p>
For the purposes of this tutorial I will just be turning off the firewall on the server, this is not recommended in a live environment and is just for tutorial purposes.
</p>
<br />

<p>
<img src="https://i.imgur.com/IiHkxu7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
after this check the client machine can ping the DC VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/p4vKEiL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now you will want to go into server manager and select Add roles and features.
</p>
<br />

<p>
<img src="https://i.imgur.com/okWtE54.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
At the server roles section select Active Directory Domain Service and continue with the installation.
</p>
<br />

<p>
<img src="https://i.imgur.com/iZL4w2k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next click the flag icon in the top right of the screen and click "Promote this server to a domain controller".
</p>
<br />

<p>
<img src="https://i.imgur.com/1hlL6FY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
select "Add a new forest" and input yourdomainname.com
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
if "Create DNS delegation" is selected, uncheck the box.
</p>
<br />

<p>
<img src="https://i.imgur.com/il1AjDD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
once complete we will now go into azure and open the network interface card associated with the Client VM and set it to use the private IP of the DC machine as its DNS server. Then restart the Client VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/uiRzu7X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now RDP into the client machine and right-click the windows logo and select "System".
</p>
<br />

<p>
<img src="https://i.imgur.com/inZ4oMD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
scroll down and click "Advanced system properties" and navigate to the tab labelled "Computer Name" and click the "Change..." button that is used to change the domain or workgroup.
</p>
<br />

<p>
input the domain name we created earlier within the DC VM to change the Client VMs domain to that of the servers. 
</p>
<br />

<p>
<img src="https://i.imgur.com/aUxs6Df.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next switch to the DC VM and open "Active Directory Users and Computers".
</p>
<br />

<p>
<img src="https://i.imgur.com/TE50NCR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to the "Users" tab and create a new user, this account will be the domain admin account used when configuring the settings from this point forward.
</p>
<br />

<p>
<img src="https://i.imgur.com/AH2cKd0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Double click the user you had just created to open the properties, select the "Member Of" tab and add the account to the "Domain Admins" group.
</p>
<br />

<p>
Now RDP into the Client VM as the domain admin you have just made by using username@domainname.com.
</p>
<br />


<p>
<img src="https://i.imgur.com/uiRzu7X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click the windows icon and select "System".
</p>
<br />


<p>
<img src="https://i.imgur.com/Bb5nSIa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
scroll down and click "Remote Desktop", then click "Select users that can remotely access this PC" and add the domain users group.
</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Congratulations, You have now setup and configured active directory in an Azure VM setting.
</p>
<br />
