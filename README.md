</p>

<h1>Performing Activities on the Network</h1>
In this walkthrough we will be performing activities on the network using Wireshark (protocol analyzer) and a bunch of command line tools. We'll be working with a few Azure resources such as a Virtual Machines (Windows 10 and Linux Ubuntu) and Network Security Groups (Firewall Resource)
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Microsoft Remote Access in the App Store for MAC users)

<h2>Operating Systems Used</h2>

- Windows Server 2022</b> (21H2)
- Linux (Ubuntu)</b> (21H2)

<h2>Setup Resources in Azure</h2>

<h2>Part 1 (Create our Resources)</h2>

Create a Resource Group
Create a Windows 10 Virtual Machine (VM)
While creating the VM, select the previously created Resource Group
While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
<img width="1440" alt="Screenshot 2023-08-01 at 10 24 49 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/f9b80d5f-80cb-4c5e-b9e0-9355a8137ed6">
<img width="1440" alt="Screenshot 2023-08-01 at 10 25 31 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/f98766ff-edde-4d89-bb75-96341b3625f7">
<img width="1440" alt="Screenshot 2023-08-01 at 10 26 21 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/1d8f4790-73d2-44c1-8083-bf2f315349ef">

Create a Linux (Ubuntu) VM
While create the VM, select the previously created Resource Group and Vnet
Observe Your Virtual Network within Network Watcher
<img width="1440" alt="Screenshot 2023-08-01 at 10 42 02 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/03229f57-b99a-4ba9-9d6f-66f6d0f9fc3f">
<img width="1440" alt="Screenshot 2023-08-01 at 10 43 03 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/72258d04-9032-4e76-8711-e858a4ec2035">

<h2>Part 2 (Observe ICMP Traffic)</h2>

Use Remote Desktop to connect to your Windows 10 Virtual Machine
Within your Windows 10 Virtual Machine, Install Wireshark by the default settings
<img width="1440" alt="Screenshot 2023-08-01 at 10 52 31 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/5cdda98d-c778-40ae-af25-bac0938ea618">
<img width="1440" alt="Screenshot 2023-08-01 at 10 57 23 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/170ec466-20d4-4dfb-ad8e-3ec63ab6179f">

Open Wireshark and filter for ICMP traffic only
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark
<img width="1440" alt="Screenshot 2023-08-01 at 11 01 30 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/8c291d7a-7397-46f1-9991-4b1223eb9f0d">

From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
<img width="1440" alt="Screenshot 2023-08-01 at 11 04 26 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/98530493-a696-42d0-bb47-8d8f9621dda6">

Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity

<img width="1440" alt="Screenshot 2023-08-01 at 11 07 45 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/b8a62bc5-b721-40f2-9dbe-d7ad3c4a4fee">
<img width="1440" alt="Screenshot 2023-08-01 at 11 09 07 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/5c9ffaf3-0cfe-4bb0-a7fa-8cbcf1c4abf0">
<img width="1440" alt="Screenshot 2023-08-01 at 11 09 07 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/3b9c9817-3a76-43f2-b1fa-c6a6cab03a2c">

Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity
<img width="1440" alt="Screenshot 2023-08-01 at 11 16 45 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/936f48cb-9fdf-4524-a8a6-2815f2e2f01a">

<h2>Part 2 (Observe SSH Traffic)</h2>

Back in Wireshark, filter for SSH traffic only
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
When entering the password, it will appear invisible
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]
<img width="1440" alt="Screenshot 2023-08-01 at 11 26 07 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/6909eb0f-aeaa-445b-9dec-e2f8698c8843">
<img width="1440" alt="Screenshot 2023-08-01 at 11 26 54 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/3605fec0-087a-46db-8e4f-0e4545b1b802">

<h2>Part 2 (Observe DHCP Traffic)</h2>

Back in Wireshark, filter for DHCP traffic only
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
Observe the DHCP traffic appearing in WireShark
<img width="1440" alt="Screenshot 2023-08-01 at 11 51 15 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/aa14e2ae-8e79-4972-9782-f91079da703c">

<h2>Part 2 (Observe DNS Traffic)</h2>

Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark
<img width="1440" alt="Screenshot 2023-08-01 at 11 56 39 AM" src="https://github.com/montrequonwheeler/Networking/assets/127397594/40f05c24-d498-477f-9301-519a81fbf500">

<h2>Part 2 (Observe RDP Traffic)</h2>

Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Oserve the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted
https://github.com/montrequonwheeler/Networking/assets/127397594/2b6f3b47-1292-4ecd-9975-1d495349028b

<h2>Lab Cleanup (DON’T FORGET THIS)</h2>

Close your Remote Desktop connection
Delete the Resource Group(s) created at the beginning of this lab
Verify Resource Group Deletion

