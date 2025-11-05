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
