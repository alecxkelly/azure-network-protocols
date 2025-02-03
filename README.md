<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create our Virtual Machines
- Configuring a Firewall (Network Security Group)
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic

  

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Begin with setting up Ip addresses from Azure into the VMs -> Assuming VMs were turned off from the day before, tick the VMs in Azure -> Press Start to begin now working in VMs -> Create a Resource Group -> Create a Windows 10 Virtual Machine (VM) using the previously created Resource Group -> adjust settings correctly -> create -> While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet -> Now, Create a Linux (Ubuntu) VM(While creating the VM, select the previously created Resource Group and Virtual Network—the Virtual Network MUST BE THE SAME) -> Authentication type: Username/Password NOT SSH public key -> Next -> Next -> Ensure both VMs are in the same Virtual Network / Subnet 


</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>If using Mac, install Microsoft Remote Desktop -> Use Remote Desktop to connect to Windows 10 Virtual Machine by getting the Ip address to put into the Microsoft VM, Install Wireshark -> Open Wireshark and start packet capture -> Within Wireshark, filter for ICMP traffic only -> Now we Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM -> Open PSH from start menu -> Now From Windows VM I will attempt to ping Linux VM -> Observe ping requests and replies within WireShark -> 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Configuring a Firewall -> Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM(ping 10.2.0.5 -t) -> enter -> Next, Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic -> Go back to Azure portal -> click on the Linux VM -> Networking -> Network settings -> Network Security Group -> click linux-vm-nsg -> settings -> Inbound Security rules to create a rule for traffic coming inbound to the VM ->  Add -> Make sure the(Destination port ranges) is an asterik * simply means any port -> protocol "ICMPv4" -> Action -> Deny -> priority(290) which will put that rule above the default rule -> Add(Can see now inbound security rules set) -> Back to PSh you will see in the terminal that "Request Timed out" means that the rule has been applied 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now to Observe SSH traffic -> Login to Microsoft Azure, Turn on the Vms you'll need to use, Login to the specified VM using the given Public Ip address if VM has been deleted -> Back in Wireshark, start a packet capture up -> Filter for SSH traffic only -> From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address) -> observe its SSH traffic -> Then I typed commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now to Observe DHCP traffic -> Back in Wireshark, filter for DHCP traffic only -> From my Windows 10 VM, I attempted to issue my VM a new IP address from the command line -> Observe the DHCP traffic appearing in WireShark
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now to Observe DNS traffic -> Back in Wireshark, filter for DNS traffic only -> From my Windows 10 VM within a command line, I used nslookup to see what google.com and disney.com’s IP addresses were -> Observe the DNS traffic being shown in WireShark
</p>  
<br />





