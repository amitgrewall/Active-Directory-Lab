<h1>Active Directory Home Lab</h1>


<h2>Description</h2>
This project demonstrates the setup and configuration of a small-scale enterprise network using Active Directory in a virtualized environment. The lab was built using Oracle VirtualBox, Windows Server 2022, and Windows 10, emulating a small corporate domain environment..

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle VirtualBox</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b> Windows Server 2022</b>
<h2>Program walk-through:</h2>


I started by confuring IP addressing for the network. The domain controller has two network interface cards, one for the internet access and one for the internal network. I manually assigned a static IP address to the internal NIC to ensure communication between the domain controller and client machine :  <br/>
<img src="https://imgur.com/RN2hBJi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
After configuring the network, I installed Active Directory Domain Services (AD DS) on the Windows Server 2019 virtual machine. I then promoted the server to a domain controller and created a new domain, which will manage user authentication and network resources within the internal network: <br/>
<img src="https://imgur.com/YcZR6EH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
To follow best practices, I created a dedicated domain administrator account instead of using the built-in Administrator account. I then created an Organizational Unit (OU) named 'ADMINS' to store admin accounts and added a new user under my name with domain admin privileges:  <br/>
<img src="https://imgur.com/OmcJg9W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Inside the 'ADMINS' Organizational Unit, I created a new user account under my name and assigned it domain administrator privileges :  <br/>
<img src="https://imgur.com/FmFpZXt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
After creating my domain admin account, I logged in using my credentials, verifying that Active Directory recognized the new user. Next, I installed Routing and Remote Access (RAS) with Network Address Translation (NAT). This setup allows the Windows 10 client on the private virtual network to access the internet through the domain controller, ensuring proper network connectivity:  <br/>
<img src="https://imgur.com/HZik6zD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Configured NAT in RAS to let the Windows 10 client access the internet through the domain controller:  <br/>
<img src="https://imgur.com/84i2zmw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Installed and configured a DHCP server on the domain controller to automatically assign IP addresses to devices on the private network. This allows the Windows 10 client to receive an IP address dynamically and access the internet, similar to how networks operate in offices or schools:  <br/>
<img src="https://imgur.com/Faegjfk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Configured a DHCP scope on the domain controller, defining the IP address range from 172.16.0.100 to 172.16.0.200 with a subnet mask of 255.255.255.0, allowing the DHCP server to assign addresses within this range to clients on the private network:  <br/>
<img src="https://imgur.com/mhXAYVn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Configured DHCP options to specify the DNS server and default gateway for clients. Since the domain controller handles NAT and routing, the Windows 10 client will use the internal NIC of the domain controller as its default gateway to access the internet:  <br/>
<img src="https://imgur.com/YgEfOz4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Used a PowerShell script to automate the creation of 1,000 sample user accounts in Active Directory, avoiding the need for manual entry. I downloaded the script from a provided link, saved it to my desktop, and executed it using the PowerShell application to populate the domain with random user accounts:  <br/>
<img src="https://imgur.com/QJmLmBk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Ran the PowerShell script, which automatically added all 1,000 user accounts to Active Directory, populating the domain with sample users for testing and management purposes:  <br/>
<img src="https://imgur.com/UysYh15.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Lastly, I created a Windows 10 virtual machine in VirtualBox with an internal NIC set to obtain an IP address from the DHCP server. I verified connectivity using the ipconfig command in Command Prompt, then joined the machine to the domain and logged in with one of the newly created Active Directory user accounts, completing the lab setup:  <br/>
<img src="https://imgur.com/UysYh15.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
