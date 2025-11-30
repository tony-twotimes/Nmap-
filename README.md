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

Step 2: Enumerate Services 

*There are several services worth enumerating here. 80/tcp, if IIS is installed, we can enumerate web content, directories, versions and exploits. 135/tcp Remote Procedure Call - a gateway to lots of Win enumeration that is necessary for SMB. 139/tcp Clasic SMB enumberation shares, users and sessions. 445/tcp This is the main service I'll focus on. Here we'll find Shares, permissions, SMB versions, users, and potential exploits. I will work on enumerating this more in a future lab; for now I'd like to continue evaluating Nmap's capabilities.*

### <img width="759" height="330" alt="image" src="https://github.com/user-attachments/assets/d7d6236e-4465-41ff-af3c-4c56e359fabb" />










