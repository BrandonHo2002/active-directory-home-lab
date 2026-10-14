# Ticket #1 - DNS Resolution Failure 

## Problem

Simulated a Help Desk incident where a domain-joined Windows 11 client 
could not resolve the mapletech.local domain name.

## Symptoms 

- The client could communicate with the domain controller using its IP address.
- The client could not resolve mapletech.local by hostname.
- nslookup mapletech.local timed out.

## Investigation

### 1. Checked the original network configuration

Reviewed the client's network configuration before simulating the issue.

- IPv4 address: 192.168.3.129
- Default gateway: 192.168.3.2
- DNS server: 192.168.3.10

### 2. Tested connectivity to the domain controller

Ran:

ping 192.168.3.10

The ping was successful, confirming that the client could communicate with the
domain controller over the network.

### 3. Tested domain name resolution

Ran:

ping mapletech.local

The hostname could not be resolved.

Then Ran:

nslookup mapletech.local

The DNS request timed out. 

### 4. Checked the DNS confirguration

Ran: 

ipconfig /all 

The client was configured to use DNS server 192.168.3.254 instead of the domain 
controller's DNS server at 192.168.3.10.

### 5. Tested the domain controller's DNS directly

Ran:

nslookup mapletech.local 192.168.3.10

The lookup succeeded, confirming that the domain controller's DNS service could 
resolve the domain name when queried directly.

## Root Cause

CLIENT01 was configurated to use the incorrect DNS server (192.168.3.254) instead 
of the domain controller's DNS server (192.168.3.10).

## Resolution

Changed CLIENT01's DNS server configuration to 192.168.3.10, the IP address
of DC01.

Flushed the local DNS cache using:

ipconfig /flushdns

## Verification

- Confirmed that nslookup mapletech.local successfully resolved the domain
  name after correcting the DNS configuraiton.
- Verified that CLIENT01 was using the domain controller's DNS server at 192.168.3.10.

## Tools used 

- Windows 11 (CLIENT01)
- Windows PowerShell
- ipconfig /all
- ipconfig /flushdns
- ping
- nslookup
- DNS on Windows server 2022 (DC01)

## Screenshots

- ticket-01-01-working-dns-configuration.png — Original working network configuration.
- ticket-01-02-dns-failure.png — Failed domain name resolution.
- ticket-01-03-dns-investigation.png — DNS configuration and direct DNS query results.
- ticket-01-04-dns-restored.png — Successful DNS resolution after the correction.

## Skills Demonstrated 

- Windows network troubleshooting
- DNS name resolution troubleshooting
- IP connectivity testing
- Network configuration verification
- PowerShell command-line troubleshooting
- Root cause identification
- Troubleshooting verification and documentation
