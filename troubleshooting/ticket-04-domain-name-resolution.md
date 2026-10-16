# Ticket #4 - DNS Name Resolution Issue

## Problem 

CLIENT01 was unable to resolve the domain name mapletech.local after its DNS
server configuration was temporarily changed during a simulated Help Desk 
troubleshooting exercise.

## Symptoms

- DNS queries for mapletech.local failed when CLIENT01 used 192.168.3.129
  as its DNS server.
- nslookup reported that the domain name could not be found and that the DNS
  server did not respond.
- The correct DNS server for the lab is DC01 at 192.168.3.10.

## Investigation

### 1. Checked the network configuration

Ran:

Get-NetIPConfiguration

Confirmed that CLIENT01 had the following configuration before the test:

- IPv4 address: 192.168.3.129
- Default gateway: 192.168.3.2
- DNS server: 192.168.3.10

### 2. Identified the active network adapter

Ran:

Get-NetAdapter

Identified Ethernet0 as the active network adapter used for the lab's 
network connection.

### 3. Checked the configured DNS server

Ran:

Get-DnsClientServerAddress -AddressFamily IPv4

Verified the DNS server configuration for CLIENT01's network adapter 
before making the change.

### 4. Simulated an incorrect DNS configuration

Temporarily changed the DNS server for Ethernet0 to 192.168.3.129, CLIENT01's 
own IP address, using:

Set-DnsClientServerAddress -InterfaceAlias "Ethernet0" -ServerAddresses 192.168.3.129

### 5. Tested DNS name resolution

Ran:

nslookup mapletech.local

The DNS query failed because CLIENT01 was using its own IP address as the DNS
server instead of the domain controller's DNS service.

### 6. Restored the correct DNS configuration

Changed the DNS server for Ethernet0 back to 192.168.3.10, the IP address 
of DC01.

## Root Cause

CLIENT01 was configured to use its own IP address (192.168.3.129) as its DNS
server instead of DC01 (192.168.3.10), which provides DNS resolution for the
lab's domain.

## Resolution

Restored the DNS server configuration on CLIENT01's Ethernet0 adapter to
192.168.3.10.

## Verification

Confirmed that CLIENT01's DNS server configuration was restored to 192.168.3.10.

- Re-ran nslookup mapletech.local and confirmed that the domain name
  resolved successfully.
- Re-ran ping DC01 and confirmed that the domain controller could be reached
  by hostname.

These checks confirmed that DNS name resolution was working correctly after the original configuration was restored.

## Tools Used

- Windows PowerShell
  - Used PowerShell commands to inspect and update network configuration.
- Get-NetIPConfiguration
  - Reviewed the IP address, default gateway, and DNS configuration.
- Get-NetAdapter
  - Identified the active network adapter.
- Get-DnsClientServerAddress
  - Checked the configured DNS server.
- Set-DnsClientServerAddress
  - Changed and restored the DNS server setting.
- nslookup mapletech.local
  - Tested DNS name resolution.
- ping DC01
  - Tested connectivity to the domain controller by hostname.

## Screenshots

- ticket-04-01-baseline-dns.png — Shows the original DNS configuration before
  the test.
- ticket-04-02-dns-failure.png — Shows the failed DNS lookup with the
  incorrect DNS configuration.
- ticket-04-03-dns-restored.png — Shows the restored DNS configuration.

## Skills Demonstrated

- Windows network configuration and troubleshooting.
- DNS name resolution troubleshooting.
- PowerShell network administration.
- Identifying and correcting an incorrect DNS server configuration.
- Verifying network settings and connectivity.
- Documenting a simulated Help Desk incident.
