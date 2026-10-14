# Ticket #2 Finance Folder Access Issue

## Problem

Michael Chen (MAPLETECH\mchen) was unable to access the Finance department shared 
folder, even though the user was expected to have access through the 
Finance_Group security group.

## Symptoms

- Michael Chen was associated with the Finance department.
- Finance_Group was not listed in Michael's group memberships during the investigation.
- Michael could not access the Finance shared folder as expected.
- The folder's permissions included Finance_Group with Modify access.

## Investigation 

### 1. Checked Michael Chen's Active Directory account

Opened Active directory Users and Computers (ADUC) and located Michael Chen's user account.

Verified that his account was associated with the Finance department.

### 2. Checked the user's security group memberships

Reviewed the Member Of tab in Michael's account properties.

Confirmed that Finance_Group was not listed among his group memberships.

### 3. Reviewed the Finance folder's permissions

Checked the NTFS security permissions configured on the Finance folder.

Confirmed that Finance_Group had Modify permissions on the folder.

### 4. Identified the missing group membership

The folder already had permissions assigned to Finance_Group, but Michael was not a 
member of that group.

This explained why he was not receiving the intended access through the security group.

### 5. Updated the user's group membership

Added Michael Chen back to Finance_Group in Active Directory.

### 6. Tested the updated access

Signed in to CLIENT01 using Michael's domain account and checked his group memberships using:

whoami /groups

Confirmed that MAPLETECH\Finance_Group appeared in the group membership information.

## Root Cause

Michael Chen was not a member of Finance_Group, which had Modify permissions on the Finance folder. As a result, he was not receiving the expected access through that security group.

## Resolution

Added Michael Chen back to Finance_Group in Active Directory.

Refreshed the user's domain session so the updated group membership could take effect.

## Verification

Tested the fix on CLIENT01 using Michael Chen's domain account.

- Confirmed that MAPLETECH\Finance_Group appeared in the user's group membership information.
- Successfully opened the Finance shared folder.
- Accessed the folder's contents.
- Created a test file inside the Finance folder.

These checks confirmed that access had been restored through the security group.

## Screenshots



## Tools Used

- Active Directory Users and Computers (ADUC)
- Windows File Explorer
- NTFS security permissions
- whoami /groups

## Skills Demonstrated

- Active Directory user account management
- Security group membership administration
- Windows file and folder permissions
- Troubleshooting group-based access issues
- Verifying domain security group membership
- Testing and documenting a Help Desk resolution
