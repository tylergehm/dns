  <img src="https://raw.githubusercontent.com/tylergehm/dns/main/dns.jpg" alt="GitHub banner" style="max-width:100%;height:auto;" />
</p>
<h1>Azure DNS Fundamentals: Managing A-Records, CNAMEs, and DNS Cache</h1>
In this Azure-based DNS exploration project, DNS (Domain Name System) translates human-readable domain names like example.com into IP addresses that computers use to communicate. You create an A-record (Address record), which maps a hostname directly to an IPv4 address. Then, observe and flush the DNS cache—a temporary local storage of resolved DNS queries to speed up repeated lookups. Finally, create a CNAME record (Canonical Name record), which aliases one domain name to another, enabling multiple services to share a single target hostname.
<br />
</p>


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command Line

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11 Pro (21H2)
- Windows 11 Home (Host Machine)

  <h2>Prequisites</h2>
- Windows Server 2025 Virtual Machine configured as Domain Controller
- Windows 11 Pro Virtual Machine configured as client

For additional information on how these virtual machines were set up, visit [Configuring Active Directory within Azure VMs](https://github.com/tylergehm/configure-ad)


<h2>Project Steps</h2>

- Step 1 - Log in to DC and Client VMs
- Step 2 - Ping the main frame
- Step 3 - Create a DNS A-record on DC for “mainframe”
- Step 4 - Change the mainframe IP Address and Flush DNS
- Step 5 - Create CNAME record

<h2>- Step 1 - Log in to DC and Client VMs</h2>

This project will be utilizing two virtual machines (VMs) that were set up in a previous project for configuring Active Directory. These VMs are being reused because the Domain Controller VM was configured as the DNS server for the client VM. </p>

To see how AD was set up, visit the project [Configuring Active Directory within Azure VMs](https://github.com/tylergehm/configure-ad) </p>

The project will begin by using Remote Desktop Connection to remotely connect into both VMs. </p>

<h2>Step 2 - Ping the main frame</h2>

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/4b78d0cd-f440-459b-8bb4-f959d224293f" /> </p>

In the client VM, Powershell was opened and used to attempt to ping mainframe. The ping failed. </p>

Mainframe is a made up name for this project. It is a name that does not have any DNS records, so this project will remedy that situation so that the client VM can successfully ping mainframe. </p>

When the computer attempts to ping a host, such as mainframe, it will first check the DNS cache in the computer memory. If that fails, then the computer will check the Local Host File on the harddrive disk. If that is not successful, then the computer will check the DNS server. </p>

<img width="1483" height="762" alt="image" src="https://github.com/user-attachments/assets/49810f86-1525-421a-8846-9dae45ca663b" /> </p>

The client VM attempted to use the command "nslookup mainframe" and was unsuccessful. Nslookup mainframe queries the DNS server to resolve the name to an IP address; it failed because mainframe has no record in DNS. </p>

This project resolves the failure by adding a record at the appropriate level to enable successful resolution and pinging. </p>

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb5aaca5-a831-482c-befa-175e9c18151c" />

This remedy begins by opening up DNS in the Domain Controller VM. </p>


