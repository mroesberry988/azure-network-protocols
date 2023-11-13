# azure-network-protocols
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>

In this step-by-step tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark(ICMP, SSH, DHCP, DNS, and RDP) as well as experiment with Network Security Groups. Wireshark is a protocol analyzer that lets us see the actual raw traffic between  the two Virtual Networks (VM's).


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

  

1) In Azure, we first need to create our Resource Group. (See Pictures Below)
2) Create a Windows 10 Virtual Machine (VM)
   a. While creating the first VM, select the resource group that was previously created.
   b. As the VM creates, allow it to create a new Virtual Network( Vnet) and Subnet
3) Next we will create the second VM. This VM will be a Linux or Ubuntu Virtual Machine
   a. While the VM is creating, select the previously created Resource Group and Virtual Network(Vnet)
4) Observe your Virtual Network within Network Watcher.

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/ebe6fcd8-6148-499f-b079-852ae5f2f119)

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/edf2c9fc-c004-4479-a234-37df62c32104)

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/3927e300-8dac-4d9e-831d-ef29cd7e58a4)

Once we have created our Resource Group and Virtual Machines in Azure we will be ready for the following steps to observe ICMP Traffic.
We first need to go into our first Virtual Machine created (VM1) to copy and paste the Private IP Address (Example highlighted in above pictures). Next, open Remote Desktop copy, and paste the IP address to connect to our Windows 10 Virtual Machine, and click connect. 
We are now on our Remote Desktop and can continue through the following steps(Photos Below):

5) Once in VM1, Install and Download Wireshark. Again, Wireshark is a tool where we can view raw traffic between the two Virtual Machines.
6) As Wireshark opens, click Ethernet, and up at the top left corner click the fin-like icon to start capturing packets. This allows us to see live traffic that is happening on our own VM1.
   a.To filter traffic so the spamming stops, we are going to go to the top left space type in ICMP, and push enter. We now see Wireshark only showing ICMP (a protocol Ping uses to test connectivity).
   b. Our next step is to "ping" VM2 and attempt to ping within the Windows 10 VM.

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/c409ea70-b37b-488b-b305-8784e31ff1a2)

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/b8dd14f7-abdb-4408-8e62-8b8beb04d547)
   
![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/ab06a9a4-7be1-4b20-81ae-e9d2fa783083)

7) Retrieve the Linux or Ubuntu Virtual Machine (VM2) and attempt to ping it from within the Windows 10 VM Remote Desktop (See Picture Below)
   a. As we either type in or Copy and Paste  (ex: 10.0.0.5), observe the ping requests and replies within Wireshark.
   b. For an exercise, in Remote Desktop Windows 10 VM, open Powershell and attempt to ping a public website such as www.google.com and observe the traffic within Wireshark.
8) Next we are going to Initiate a non-stop ping from Windows 10 (VM1) and  Linux/Ubuntu (VM2)
   a.Enter the VM 2 Private IP address (10.0.0.5)-t
   b.While "pinging" we are going to change the firewall on VM2 to not allow ICMP Traffic to come through. As we do this, we will see the connection between VM1 and VM2 stop "Pinging".  

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/d988f467-ff7e-4a4c-b52a-6e677c45c2ce)

9) You are doing great! We are almost complete with observing ICMP Traffic. Lastly in Azure, we are going to search Network Security Group within our Linux/Ubuntu (VM2). (Photos Below)
   a.Scroll down to Inbound Security Rules. We can now observe when we Add Rule/ Deny Rules.
   b.We are going to Allow Rule and observe the Network Security Rule to receive responses from VM2. 
![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/f66a50ab-bfd5-4b2e-8ec7-ee86d36b5ec1)

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/09a86497-ad40-42cb-995a-6bfa8f144105)

Below we will now observe SSH, DHCP, DNS, and RDD data in Wireshark, and Powershell:

Observing SSH:
As we explore SSH traffic we connect VM1 to VM2 via SSH. First, we open Powershell and type in SSH with the username created when creating VM2. Continuing in Powershell, we enter the IP Private address of VM2

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/1810ae20-6a65-434b-a9c9-f10ff522a172)

Observing DHCP:

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/f40284a2-7254-4b79-ba0a-582f682767f2)

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/477ae1e6-9ac2-4325-a78d-83cd1aefe6e6)

Observing DNS:
![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/f982281a-9908-4ddd-b28c-ba4fb8d8c81d)

![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/f76a9aaa-043f-4496-93be-730c134bea8e)

Observing RDP:
![image](https://github.com/mroesberry988/azure-network-protocols/assets/134666751/f63bffb2-f9c8-47eb-8228-9aca6f0a25e7)








