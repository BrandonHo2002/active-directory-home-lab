Ticket #3 - Domain Account Lockout

Problem

Michael Chen (MAPLETECH\mchen) was unable to sign in to the domain after his 
account became locked following multiple incorrect password attempts.

Symptoms 

- Michael Chen was unable to sign in to CLIENT01.
- After multiple incorrect password attempts, Windows indicated that the account
  was locked.
- The account could no longer be used to authenticate to the domain.

Investigation

1. Configured the domain account-lockout policy in Group Policy Management for lab testing.
2. Simulated a user account lockout on CLIENT01 by entering an incorrect password three times.
3. Confirmed that Windows reported the account as locked.
4. Opened Active Directory Users and Computers (ADUC) on DC01.
5. Located Michael Chen's account and verified its locked status.
6. Reviewed the Default Domain Policy and confirmed the account-lockout threshold was set to three invalid logon attempts.

Tools / Commands used 

- Active Directory users and Computers (ADUC)
    - Checked the user's account status
    - Unlocked the user's account
- Group Policy Management
    - Reviewed the domain account-lockout policy
- Windows PowerShell
    - Used whoami to verify the authentication domain account
- CLIENT01
    - Used to reproduce and verify the login problem

Root Cause 

The account was locked because three consecutive invalid password attempts 
triggered the domain's account-lockout policy.

The configured policy locks an account after 3 invalid logon attempts.

Resolution

The Michael Chen account was unlocked through Active Directory Users and
Computers.

After the account was unlocked, Michael was able to sign in to CLIENT01 
using his correct domain credentials.

Verification

Michael successfully logged into CLIENT01 after the account was unlocked.

The whoami command was used in PowerShell to confirm that the logged-in 
account was:

MAPLETECH\mchen

This confirmed that domain authentication was working again.

Skills Demonstrated 

- Active Directory account management
- Troubleshooting domain account lockouts
- Active Directory Users and Computers
- Group Policy Management
- Account-lockout policies
- Domain authentication troubleshooting
- Windows PowerShell
- User account recovery
- Incident investigation and verification
