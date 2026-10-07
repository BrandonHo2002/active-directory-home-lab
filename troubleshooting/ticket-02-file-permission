Ticket #2 file permission

Problem
Michael Chen (MAPLETECH\mchen) was unable to access the Finance department shared 
folder on the domain network, even though the user was expected to have access 
through the Finace_Group security group.

Symptoms

- Micheal Chen was a memeber of the Finace department 
- Michael Chen was not showing as a memeber of Finance_Group during the investigation
- The Finance folder was not recieving the expected group-based permissions, he
- could not access the Finance folder as intended.

Investigation 

1. Checked Michael Chen's user account in Active directory.
2. Verified that Michael Chen was associated with the Finance department.
3. Checked the user's Member of group memeberships.
4. Confirmed that Finance_Group was not listed as one of Michael Chen's 
   memberships.
5. Reviewd the permissions configured on the Finance folder.
6. Confirmed that Finance_Group had Modify permissions on the Finance folder.
7. Removed/reviewed the user's group memebership configuration as part of 
   troubleshooting.
8. Added Michael Chen back to Finance_Group.
9. Logged into the CLIENT01 workstation using Michael's domain account and
   verifed the updated group memebership.

Tools/Commands Used

- Active Directory Users and Computers (ADUC)
  - User account management
  - Security group memebership
- Windows File Explorer
  - Finance folder access testing 
  - File creation testing
- NTFS Security Permissions
  - Verifed Finance_Group permissions
- whoami /groups
  - Verified the security groups assigned to the logged-in user

Root Cause

Michael Chen was not receiving the expected permissions from Finance_Group 
because he was not currently a member of that security group.

The Finance folder relied on group-based permissions rather than assigning
permissions directly to Michael Chen.

Resolution 

Michael Chen was added back to Finance_Group security group.

After the group memebership was updated, the user's domain session was refreshed 
so that the updated group memebership could take effect.

Verification

The fix was tested by logging in as Michael Chen on CLIENT01.

The MAPLETECH\Finance_Group memebership was confirmed, and Michael was able to:
  - Open the Fiancce folder.
  - Access its contents
  - Create a test file inside the Finance folder.

This confirmed that the user's access had been successfully restored through 
the security group.

Skills Demonstrated

- Active Directory user management
- Active Directory security group management 
- Troubleshooting group-based access
- MTFS permissions
- Windows file-system permissions
- Domain authentication
- Verifying security group membership
- Basic Help Desk troublshooting methodology
- Testing and documenting a successful resolution
