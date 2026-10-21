# Ticket #1 - DNS Resolution Failure 

## Problem

Simulated a Help Desk incident in a domain-joined Windows 11 environment where
the client could not resolve the mapletech.local domain name. The scenario was
used to practice DNS troubleshooting and identify an incorrect client DNS
configuration.

## Symptoms 

- The client could communicate with the domain controller using its IP address.
- The client could not resolve mapletech.local by name.
- DNS lookup attempts using the client's configured DNS server timed out.

## Investigation

### 1. Recorded the initial working network configuration

Recorded CLIENT01's network configuration before introducing the 
simulated DNS issue.

- IPv4 address: 192.168.3.129
- Default gateway: 192.168.3.2
- DNS server: 192.168.3.10

The initial configuration was working correctly, with CLIENT01 using the domain controller (192.168.3.10) as its DNS server. An incorrect DNS server configuration was then introduced to simulate a Help Desk incident.

### 2. Tested connectivity to the domain controller

Ran:

  ping 192.168.3.10

The ping was successful, confirming that the client could communicate with the
domain controller over the network.

### 3. Tested domain name resolution

Ran:

  ping mapletech.local

The hostname could not be resolved.

Then ran:

  nslookup mapletech.local

The DNS request timed out when using the client's configured DNS server.

### 4. Inspected the client's DNS configuration

Ran: 

  ipconfig /all 

The output showed that CLIENT01 was configured to use DNS server 192.168.3.254 
instead of the domain controller's DNS server at 192.168.3.10.

### 5. Tested the domain controller's DNS directly

Ran:

  nslookup mapletech.local 192.168.3.10

The lookup succeeded, confirming that the domain controller's DNS service could 
resolve the domain name when queried directly.

## Root Cause

CLIENT01 was configured to use the incorrect DNS server (192.168.3.254) instead
of the domain controller's DNS server (192.168.3.10). As a result, the client
could not successfully resolve the domain name using its configured DNS server.

## Resolution

Corrected CLIENT01's DNS server configuration to use 192.168.3.10, the IP 
address of DC01, instead of the incorrect DNS server at 192.168.3.254.

Flushed the local DNS cache using:

  ipconfig /flushdns

## Verification

- Confirmed that nslookup mapletech.local successfully resolved the domain
  name after correcting the DNS configuration.
- Verified that CLIENT01 was using the domain controller's DNS server at
  192.168.3.10.

## Tools Used 

- Windows 11 (CLIENT01)
- Windows PowerShell
- ipconfig /all
- ipconfig /flushdns
- ping
- nslookup
- DNS on Windows server 2022 (DC01)

## Screenshots

- ticket-01-01-working-dns-config.png — Original working network
  configuration before the simulated issue.
- ticket-01-02-dns-failure.png — Failed domain name resolution using the
  incorrect DNS configuration.
- ticket-01-03-dns-investigation.png — Direct DNS query to the domain controller.
- ticket-01-04-dns-resolved.png — Successful DNS resolution after correcting
  the DNS configuration.

## Skills Demonstrated 

- Windows network troubleshooting
- DNS name resolution troubleshooting
- IP connectivity testing
- Network configuration verification
- PowerShell command-line troubleshooting
- Root cause identification
- Troubleshooting verification and documentation
