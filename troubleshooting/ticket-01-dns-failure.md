Ticket 01 - DNS Resolution Failure 

Problem

Simulated a Help Desk incident where a domain-joined Windows 11 client 
could not resolve the mapletech.local domain name

Symptoms 

- The client could communicate with the domain controller using its IP address.
- The client could not resolve mapletech.local by hostname
- nsloopkup mapletech.local timed out.

Investigation

1. Checked the working network configuration

Verified the client's original network configuration before simulating the issue.

- IPv4 address: 192.168.3.129
- Default gateway: 192.168.3.2
- DNS server: 192.168.3.10

2. Tested connectivity to the domain controller

ping 192.168.3.10

The ping was successful, confirming that the client could communicate with the
domain controller over the network.

3. Tested domain name resolution

ping mapletech.local

The hostname could not be resolved.

Then tested DNS directly:

nslookup mapletech.local

The request timed out. 

4. Checked the DNS confirguration

ipconfiguration /all The client was configured to use: 

192.168.3.254

instead of the domain controller's DNS server. 

5. Tested the domain controller's DNS directly

nslookup mapletech.local 192.168.3.10

The lookup succeeded.

This confirmed that the domain controller's DNS service was working and that
the problem was with the client's configured DNS server. 

Root Cause

The CLIENT01 DNS configuration was pointing to the incorrect DNS server 
(192.168.3.254) instead of the domain controller's DNS server (192.168.3.10).

Resolution

Changed the CLIENT01 DNS server back to:

192.168.3.10

Then flushed the local DNS cache:

ipconfig /flushdns

Verification

Confirmed that DNS resolution was working again: 

nslookup mapletech.local

The domain name successfully resolved through the domain controller's DNS server.

Tools used 

- Windows 11
- PowerShell
- ipconfig /all
- ipconfig /flushdns
- ping
- nslookup
- Active Directory Domain Services
- DNS

Screenshots

1. Working DNS configuration
2. DNS failure
3. DNS investigation and root cause
4. DNS resolution restored

Skills Demonstrated 

- Basic Windows network troubleshooting
- DNS troubleshooting
- IP connectivity testing
- DNS coniguration verification
- PowerShell troubleshooting commands
- Root-cause identifcation
- Troubleshooting verification and documentation
