## OVERVIEW
This lab covers deploying and managing Windows Server 2022 Virtual Machines in Microsoft Azure using Infrastructure as a Service (IaaS). Throughout the project, I configured virtual network interfaces, assigned static public IPs, established Remote Desktop Protocol (RDP) connections for cloud administration, and executed network diagnostic commands to simulate real-world help desk troubleshooting scenarios.

## ENVIRONMENT BUILT
* **Resource Group Name:** helpdesk-lab1
* **VM Name:** vm-helpdesk1
* **OS Used:** Windows Server 2022 Datacenter - x64 Gen 2
* **Region:** West US 2
* **Size:** Standard_B2ats_v2
* **Public IP:** Static (configured for remote accessibility via RDP)

### 1. Resource Group Creation
* Started by creating a new Resource Group in the East US region and named it helpdesk-lab1 to organize all related lab assets.
* <img width="1880" height="770" alt="Screenshot 2026-09-29 190528" src="https://github.com/user-attachments/assets/449c7f0f-151f-4994-88e5-403ccd119d0a" />

### 2. VM Configuration & Cost Review
* Configured the virtual machine with no infrastructure redundancy and standard security type. Chose Windows Server 2022 Datacenter-x64 Gen 2 for the OS, selecting a free service tier option (Standard_B2ats_v2).
* <img width="1001" height="807" alt="Screenshot 2026-09-29 193350" src="https://github.com/user-attachments/assets/de0ed9e0-dcf6-4d47-9fc3-563a6c0d77d8" />

### 3. Deployment & Handling Errors
* Addressed initial capacity restrictions in the East US region by switching the deployment location to West US 2.
* Resolved a disk configuration mismatch (manually specified a 64 GB disk versus the required 127 GB default image size) by restarting the deployment cleanly with the correct specs in West US 2.
* <img width="1310" height="399" alt="Screenshot 2026-09-29 193715" src="https://github.com/user-attachments/assets/081b7cae-8b2f-4ef5-87b1-b463305ef61e" />

### 4. Configuring Static Public IP
* Navigated to the networking tab of vm-helpdesk1 and changed the public IP address assignment from dynamic to static to ensure persistent remote access.
* <img width="568" height="897" alt="Screenshot 2026-09-29 193850" src="https://github.com/user-attachments/assets/9128bd0f-5c9d-4e1d-a990-30c9890006ce" />

### 5. Resource Status & Remote Connection
* Verified all resources were active in Azure, then established an RDP connection from my local machine using the VM's static public IP and administrator credentials (vm-helpdesk1\helpdesk-admin).
* <img width="1862" height="858" alt="Screenshot 2026-09-29 194143" src="https://github.com/user-attachments/assets/d3e09717-4a41-4b6d-8faf-f5bf239fdfe7" />

### 6. Network Diagnostic Commands Execution
* Opened the Command Prompt inside the remote session and ran network diagnostic commands to simulate help desk troubleshooting:
  * **ipconfig**: Checked basic IP configuration (valid addresses, no APIPA 169.254 or 0.0.0.0 gateway errors).
  * **ipconfig /all**: Displayed full TCP/IP configuration, MAC address, DHCP status, and DNS servers.
  * **ping 127.0.0.1**: Tested the local loopback NIC (0ms latency, confirming healthy stack).
  * **ping google.com**: Tested external internet access and DNS resolution (~4ms latency).
  * **tracert google.com**: Traced network transit hops out to the internet.
  * **nslookup google.com**: Queried DNS to successfully resolve the domain name.
  * **netstat**: Displayed active network connections, verifying port 3389 was actively listening for RDP.
<img width="1691" height="840" alt="Screenshot 2026-09-29 194858" src="https://github.com/user-attachments/assets/f9a3b5a7-a6f3-4ce4-9636-a6df0a95001b" />
<img width="733" height="487" alt="image" src="https://github.com/user-attachments/assets/1a6b4cb4-25b3-423f-aef8-7d309922fdb9" />
<img width="581" height="277" alt="Screenshot 2026-09-29 195411" src="https://github.com/user-attachments/assets/be1c0997-7d76-4f09-a9cf-d8bb6471216c" />
<img width="520" height="204" alt="image" src="https://github.com/user-attachments/assets/9a4cd3e0-ee4f-4404-ba0f-34f239750e15" />
<img width="644" height="302" alt="Screenshot 2026-09-29 195930" src="https://github.com/user-attachments/assets/39552609-85e2-4d07-9f07-d72a93fb2117" />
<img width="448" height="158" alt="image" src="https://github.com/user-attachments/assets/fdbac420-574e-45d2-b5a9-2fed08f2612a" />
<img width="673" height="407" alt="image" src="https://github.com/user-attachments/assets/c8f3b28d-1c34-4f07-b279-de8a8955a02c" />

## ERRORS ENCOUNTERED & RESOLVED
* **Capacity Restriction Error**
  * **Cause:** Attempted to deploy Standard_B2ats_v2 in a region lacking capacity.
  * **Fix:** Switched the deployment region to West US 2.
* **Disk Configuration Conflict**
  * **Cause:** Manually specified a 64 GB disk size, which was smaller than the default 127 GB requirement for the Windows Server image.
  * **Fix:** Restarted the deployment from scratch with the correct configuration.

## KEY CONCEPTS LEARNED
* **IaaS Provisioning:** Deploying and scaling virtualized cloud infrastructure, resource groups, and regions.
* **IP Addressing & Networking:** Utilizing static public IPs for persistent remote accessibility.
* **RDP Management:** Administering cloud-based Windows environments securely over port 3389.
* **Troubleshooting Diagnostics:** Applying diagnostic tools (ipconfig, ping, tracert, nslookup, netstat) to validate interface health, local routing, DNS resolution, and active ports. 
