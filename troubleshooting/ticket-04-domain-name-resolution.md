Ticket #4 - DNS Name Resolution Issue

Problem 

CLIENT01 was unable to resolve the domain name mapletech.local after its DNS
server configuration was temporaily changed during a simulated Help Desk 
troubleshooting excercise.

Symptoms

- DNS queries for mapletech.local failed when CLIENT01 used 192.168.3.129
  as its DNS server.
- nslookup reported that the domain name could not be found and that the
  DNS server did not respond.
- The correct DNS server for the lab is DC01 at 192.168.3.10

Investigation

1. Checked the network configuration on CLIENT01 using Get-NetIPConfiguration.
2. Confirmed that CLIENT01 had IPv4 address 192.168.3.129, default gateway
   192.168.3.2, and DNS server 192.168.3.10 before the test.
3. Used Get-NetAdapter to identify the active network adapter, ethernet0.
4. Temporarily changed the DNS server to 192.168.3.129 to simulate an
   incorrect DNS configuration.
5. Ran nslookup mapletech.local and observed that the DNS query failed.
6. Restored the DNs server to 192.168.3.10

Tools / Commands Used

- Get-NetIPConfiguration - reviewed the IP address, gateway, and
  DNS configuration.
- Get-NetAdapter - identified the active network adapter.
- Get-DnsClientServerAddress - checked the configured DNS server.
- Set-DnsClientServerAddress - changed and restored the DNS server setting.
- nslookup mapletech.local - tested DNS name resolution.
- ping  DC01 - tested connectivity to the domain controller by hostname.

Root Cause

The simulated DNs failure was caused by configuring CLIENT01 to use 
192.168.3.129 as its DNS server instead of the domain controller's DNS 
service at 192.168.3.10.

resolution

Restored the DNS server configuration on CLIENT01's Ethernet0 adapter 
to 192.168.3.10, the IP address of DC01.

Verification

- Confirmed that CLIENT01's DNS server configuration was restored
  to 192.168.3.10.
- Re-ran nslookup mapletech.local to verify DNs resolution.
- re-ran ping DC01 to check connectivity to the domain controller.
- Captured screenshots showing the initial configuration, simulated DNs failure,
  and restored configuration.

Skills Demonstrated

- Windows network configuration and troubleshooting.
- DNS name resolution and basic networking concepts.
- PowerShell administration.
- Identifying and correcting an incorrect DNS server configuration.
- Verifying connectivity and documenting a simulated Help Desk incident.
