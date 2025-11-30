# Nmap

## Objective
Evaluate several features of Nmap, including host discovery, port scanning, and service enumeration

### Skills Learned

- Built and configured a vulnerable Windows host to understand real-world attack surfaces and misconfigurations.
- Performed host discovery and port scanning with Nmap to identify live systems, open ports, and exposed services.
- Enumerated Windows services (SMB, RDP, WinRM, RPC) and analyzed the security implications of each.
- Used the Nmap Scripting Engine (NSE) to gather detailed service info, detect vulnerabilities, and run SMB-focused scripts.
- Observed how weak configurations (SMBv1, anonymous shares, open RDP, loose firewall rules) appear to attackers during recon.
- Documented findings and built a repeatable pentesting workflow from discovery → enumeration → vulnerability identification.

### Tools Used

- Nmap
- Powershell (to configure victim machine)


## Steps

Step 1: Port Scan Vulnerable Windows system

### <img width="599" height="287" alt="image" src="https://github.com/user-attachments/assets/92a76cb5-0f92-4add-aa83-f83307af6618" />

Why I Ran This

This is the initial surface-level scan to identify what common TCP ports are open on the target. It provides a quick picture of:

- which services are exposed
- whether the host is alive
- whether the network path is normal (no firewalls blocking)
- This is the first step my recon workflow.

What It Revealed:

We discovered:

- SSH (22)
- HTTP (80)
- MSRPC (135)
- NetBIOS (139)
- SMB (445)
- WSDAPI (5357)

This confirms the host is Windows-based and running classic Windows services (SMB, RPC).
It also showed that SSH is unexpectedly enabled, which is unusual for Windows.


Step 2: Targeted Port and Version Scan

### <img width="759" height="330" alt="image" src="https://github.com/user-attachments/assets/d7d6236e-4465-41ff-af3c-4c56e359fabb" />

Why I Ran This

Once the first scan found open ports, this second scan focuses on:

- Only the interesting ports
- Service versions running on those ports
- More detailed fingerprints

The purpose is to validate the initial findings and gather actionable information:

- What version of IIS?
- What version of SMB?
- What type of RPC service?
- What OS fingerprint emerges?

The goal is to  move from discovery to enumeration.

What It Revealed

Now we know:

- Port 80 → Microsoft IIS 10.0 (confirms a Windows 10 / Server 2016+ environment)
- Port 135 → Microsoft Windows RPC
- Port 139 → NetBIOS (SMBv1-related traffic)
- Port 445 → SMB (active windows file-sharing service)

Step 3: OS Detection & Aggressive Enumeration 

### <img width="794" height="696" alt="image" src="https://github.com/user-attachments/assets/c6aafcda-2d76-481a-b4ed-e90b6232d1b4" />

Why I Ran This

After identifying open ports and service versions, my next thoughts are to

- fingerprint the operating system
- identify Windows build family
- probe for network distance (hops)
- gather banner details
- run Nmap default scripts automatically

-A is aggressive enumeration, combining:

- OS detection
- version detection
- script scanning
- traceroute

This helps confirm the host is truly Windows and gives more information about potential vulnerabilities.

Step 4: HTTP Service Enumberation Using NSE 


### <img width="607" height="293" alt="image" src="https://github.com/user-attachments/assets/58d8a508-6efc-4c96-9eac-e9d156c47e35" />

I used Nmap’s http-title and http-headers NSE scripts to perform light enumeration of the HTTP service running on port 80. This step gathers mnetadata about the web server without performing intrusive testing, which confirms: 

- the web technology being used
- default configuration details
- any security headers present or missing
- whether the site is running a default, custom, or vulnerable app

I find that The host is running Microsoft IIS 10.0, confirming a modern Windows environment. The default IIS landing page is still present (http-title: IIS Windows).Response headers show no obfuscation or security hardening. No additional directories 
or custom content were revealed at this stage.


Step 5: Default Script Scan 

### <img width="833" height="498" alt="image" src="https://github.com/user-attachments/assets/d17f6a2f-00a1-4f42-ba9b-bbee23b37957" />



For the final step, I ran Nmap’s default script and version detection scan. This gave me a complete snapshot of the target’s exposed services without going into tool-specific enumeration. The scan confirmed Microsoft IIS 10.0 on port 80, Microsoft RPC on port 135, and SMB services on ports 139 and 445. Nmap also identified a common SMB misconfiguration where message signing is enabled but not required. That’s useful security context, but still within the scope of Nmap’s built-in capabilities.

Step 5 is the last step because it represents the point where Nmap has done everything it reasonably can: it has discovered ports, identified services and versions, performed OS detection, and run all the default safe scripts. Going any further would move into deeper SMB enumeration, which is best handled by tools like smbclient in a dedicated SMB lab. At this point, Nmap has provided all the recon information I need before switching to service-specific tools.

This concludes the Nmap lab. My next phase will focus on SMB enumeration using smbclient.








