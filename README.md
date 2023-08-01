</p>

<h1>Networking</h1>
This walkthrough focuses on Building Intuition for DNS after the install configuration of Microsoft Active Directory Domain Services.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Microsoft Remote Access in the App Store for MAC users)
- Active Directory Domain Services

<h2>Operating Systems Used</h2>

- Windows Server 2022</b> (21H2)
- Windows 10</b> (21H2)

<h2>Setup Resources in Azure</h2>

- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
- Take note of the Resource Group and Virtual Network (Vnet) that get created at this time

<h2>A-Record Exercise</h2>

- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
- Connect/log into Client-1 as an admin (mydomain\jane_admin)
- From Client-1 try to ping “mainframe” notice that it fails
- Nslookup “mainframe” notice that it fails (no DNS record)
- Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address
- Go back to Client-1 and try to ping it. Observe that it works

<h2>Local DNS Cache Exercise</h2>

- Go back to DC-1 and change mainframe’s record address to 8.8.8.8
- Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address
- Observe the local dns cache (ipconfig /displaydns)
- Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty
- Attempt to ping “mainframe” again. Observe the address of the new record is showing up

<h2>CNAME Record Exercise</h2>
