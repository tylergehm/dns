  <img src="https://raw.githubusercontent.com/tylergehm/dns/main/dns.jpg" alt="GitHub banner" style="max-width:100%;height:auto;" />
</p>
<h1>Azure DNS Fundamentals: Managing A-Records, CNAMEs, and DNS Cache</h1>
In this Azure-based DNS exploration project, DNS (Domain Name System) translates human-readable domain names like example.com into IP addresses that computers use to communicate. You create an A-record (Address record), which maps a hostname directly to an IPv4 address. Then, observe and flush the DNS cache—a temporary local storage of resolved DNS queries to speed up repeated lookups. Finally, create a CNAME record (Canonical Name record), which aliases one domain name to another, enabling multiple services to share a single target hostname.
<br />
</p>


<h2>Video Demonstration</h2>

- ### [YouTube: Azure DNS Fundamentals : Managing A Records, CNAMEs, and DNS Cache](https://www.youtube.com/watch?v=NE--I7QS-uo)

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

<h2>Step 3 - Create a DNS A-record on DC for “mainframe”</h2>

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb5aaca5-a831-482c-befa-175e9c18151c" />

This remedy begins by opening up DNS in the Domain Controller VM. DNS was automatically installed when the Domain Controller VM was set up as Domain Controller. </p>

<img width="942" height="660" alt="image" src="https://github.com/user-attachments/assets/f625d633-5768-4273-a716-01079c2fb02a" /> </p>

Once inside the DNS Manager, click the drop down arrows to open up DC-1 > Forward Look Up Zones > mydomain.com </p>

Located here are the A-records found within the DNS server. A-records (Address records) are entries that map hostnames (like dc-1, client-1, or mainframe) to their IPv4 addresses (e.g., 10.0.1.4). These records allow clients to resolve names to IPs using the domain’s DNS server, enabling successful pings and network communication. </p>

<img width="1483" height="762" alt="image" src="https://github.com/user-attachments/assets/976892b2-5e40-4de3-babe-d1080d2328b8" /> </p>

Next, Powershell is used to run the command "ipconfig". Located here is the IPv4 Private IP Address for the Domain Controller is 10.0.1.4. This will be used to create a A-record for mainframe with that IPv4 address. </p>

<img width="1918" height="1080" alt="image" src="https://github.com/user-attachments/assets/911dc6f3-f52b-4b5b-8404-ab126142ebfd" /> </p>

Returning to the DNS Manager, right click and select "New Host (A or AAAA)..." </p>

<img width="428" height="474" alt="image" src="https://github.com/user-attachments/assets/3db8c74e-1739-422e-b92a-14a8c0246262" />

Inside the New Host box, enter "mainframe" as the Host Name and "10.0.1.4" as the IP Address. Check the box next to "Create associated pointer (PTR) record". This will allow reverse nslookup to identify a name to an IP address.  </p>

<img width="500" height="214" alt="image" src="https://github.com/user-attachments/assets/645cfd3f-aa14-41fd-86a5-f913428be23f" /> </p>

The A-record for mainframe has successfully been created. </p>

<img width="1483" height="762" alt="image" src="https://github.com/user-attachments/assets/afa6b60b-5f47-491a-9e42-e5596811d051" /> </p>

Returning to the client VM, Powershell is used to attempt to ping mainframe again. This time the ping is successful indicating the A-record has been established </p>

<h2>Step 4 - Change the mainframe IP Address and Flush DNS</h2>

<img width="927" height="645" alt="image" src="https://github.com/user-attachments/assets/3cb1f316-945d-4907-97af-26187a250cd0" />

In the DC VM, the DNS Manager is reopened to access the A-record for mainframe. The IP address for mainframe is changed to "8.8.8.8", which is Google's IP address. </p>

<img width="1483" height="762" alt="image" src="https://github.com/user-attachments/assets/9e6131cb-53c5-4e99-8ea0-3130b430cca5" /> </p>

Back on the client VM, when "ping mainframe" command is entered into Powershell; it returns the old IP Address on the mainframe A-record. This is because the old IP Address is stored in the DNS cache of the client VM. </p>

<img width="1035" height="1010" alt="image" src="https://github.com/user-attachments/assets/a1c9b01a-307d-4e20-b0ed-8891762a5794" /> </p>

Running the command "ipconfig /displaydns" will show the DNS cache for the client VM. Here, it is shown that the DNS cache has mainframe recorded with the old IP Address. </p>

<img width="1184" height="1020" alt="image" src="https://github.com/user-attachments/assets/4d0aeb3f-2566-41cc-ae8b-3cdcbc608506" /> </p>

Opening up Powershell as Admin, the command "ipconfig /flushdns" was entered. This command clears out the DNS cache on Client VM. After, the command "ipconfig /displaydns" was entered. The results show that mainframe is no longer stored in the DNS cache. </p>

<img width="1242" height="620" alt="image" src="https://github.com/user-attachments/assets/7429cd9a-e209-40ac-be96-0556f18a1b17" /> </p>

After the DNS cache was flushed, using the "ping mainframe" command shows the updated IP Address for mainframe A-record. </p>

<h2>Step 5 - Create CNAME record</h2>

The final step in this project is to return to the Domain Controller VM and create a CNAME record. A CNAME record matches one human readable name to another human readable name. </p>

<img width="1917" height="1080" alt="image" src="https://github.com/user-attachments/assets/1f84c4e7-6a6f-4274-b836-3947fe39dc7c" /> </p>

Returning to the DNS Manager, right-click and select "Create New Alias (CNAME)..." </p>

<img width="494" height="566" alt="image" src="https://github.com/user-attachments/assets/39f178f4-e6b7-4c23-9824-a19cb6c92c91" /> </p>

In the New Resource pop up, the Alias name is labeled "search" and the fully qualified domain name that it is mapped to is "www.google.com". Then click "OK". </p>

<img width="1920" height="1076" alt="image" src="https://github.com/user-attachments/assets/9f60a5bd-05a3-4f30-ad11-26ed8c993d94" /> </p>

On the client VM, using Powershell the command "ping search" was entered. The results show a successful ping to google.com. </p>

<img width="1260" height="626" alt="image" src="https://github.com/user-attachments/assets/39cc8715-2e01-43ae-af91-bbe55732b4cb" /> </p>

The command "nslookup search" was entered into Powershell. The results show that the Domain Controller resolved the nslookup to google.com and listed IPv6 and IPv4 Addresses connected to google.com. </p>

<h2>Conclusion</h2>

This Azure DNS lab solidifies core Domain Name System concepts by configuring A-records to map hostnames to IPs, demonstrating CNAME records for aliasing, and mastering DNS cache behavior with ipconfig /flushdns. By resolving failed pings through record creation, observing stale cache effects, and enabling seamless name-to-name redirection (e.g., search → www.google.com), the project mirrors real-world DNS administration within an Active Directory-integrated environment. These skills—troubleshooting resolution failures, managing authoritative records, and ensuring name consistency—are foundational for network reliability, service accessibility, and scalable infrastructure in enterprise and cloud deployments.













