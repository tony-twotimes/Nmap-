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

*There is an HTTP service running on port 80 that we can enumerate*

### <img width="757" height="226" alt="image" src="https://github.com/user-attachments/assets/d19eb017-aaaa-4f8b-8105-77655c842a84" />







