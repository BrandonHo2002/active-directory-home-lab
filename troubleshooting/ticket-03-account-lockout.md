# Ticket #3 - Domain Account Lockout

## Problem

Simulated a Help Desk incident where Michael Chen (MAPLETECH\mchen) could not sign in 
to the domain after his account became locked following multiple incorrect password attempts.

## Symptoms 

- Michael Chen was unable to sign in to CLIENT01.
- After three incorrect password attempts, Windows indicated that the account
  was locked.
- The locked account could not be used to authenticate to the domain until it was unlocked.

## Investigation

### 1. Reviewed the domain account-lockout policy

Opened Group Policy Management on DC01 and reviewed the account-lockout settings in the 
Default Domain Policy.

Confirmed that the account-lockout threshold was configured for three invalid logon attempts.

### 2. Tested the account-lockout policy

Used CLIENT01 to simulate an account lockout by entering an incorrect password three times 
for Michael Chen's domain account.

Windows reported that the account was locked.

### 3. Checked the user's account status

Opened Active Directory Users and Computers (ADUC) on DC01.

Located Michael Chen's account and verified that it was locked.

### 4. Unlocked the account

Unlocked Michael Chen's account through Active Directory Users and Computers.

### 5. Tested domain authentication

Returned to CLIENT01 and signed in using Michael Chen's correct domain credentials.

Opened PowerShell and ran:

whoami

The command returned:

mapletech\mchen

This confirmed that the user had successfully signed in with the domain account.

## Root Cause

Michael Chen's account was locked after three invalid password attempts triggered 
the domain's account-lockout policy.

The Default Domain Policy was configured to lock an account after three invalid 
logon attempts.

## Resolution

Unlocked Michael Chen's account through Active Directory Users and Computers on DC01.

Michael was then able to sign in to CLIENT01 using his correct domain credentials.

## Verification

- Confirmed that Michael Chen's account was unlocked in Active Directory Users and Computers.
- Successfully signed in to CLIENT01 using Michael's domain credentials.
- Ran whoami in PowerShell and confirmed that the logged-in account was mapletech\mchen.

These checks confirmed that access to the domain account had been restored.

## Tools used 

- Group Policy Management
  - Reviewed the domain account-lockout policy.
- Active Directory Users and Computers (ADUC)
  - Checked the user's account status.
  - Unlocked the account.
- Windows PowerShell
  - Used whoami to verify the logged-in domain account.
- CLIENT01 (Windows 11 Pro)
  - Reproduced the account-lockout condition and verified successful sign-in.

## Screenshots

- ticket-03-01-account-locked.png — Shows the account-lockout message on CLIENT01.
- ticket-03-02-account-locked-aduc.png — Shows Michael Chen's locked account in Active
  Directory Users and Computers.
- ticket-03-03-account-lockout-policy.png — Shows the configured account-lockout policy.
- ticket-03-04-account-unlocked.png — Shows the account after it was unlocked.
- ticket-03-05-account-access-restored.png — Shows successful domain sign-in and the
  whoami result.

## Skills Demonstrated 

- Active Directory account management
- Troubleshooting domain account lockouts
- Group Policy Management
- Account-lockout policy configuration and verification
- Domain authentication troubleshooting
- Windows PowerShell command-line verification
- User account recovery
- Incident investigation and documentation
- Windows PowerShell
- User account recovery
- Incident investigation and verification
