# 02 — Active Directory User Support

## Scenario

A new employee needs an account and access to the correct group. A second scenario covers a password problem and an offboarding request.

## Environment

Windows / Active Directory lab / PowerShell fundamentals

## User & Group Verification

When the Active Directory PowerShell module is available:

```powershell
Get-ADUser -Identity testuser -Properties Enabled,LockedOut,PasswordLastSet
Get-ADPrincipalGroupMembership testuser | Select-Object Name
Get-ADGroupMember -Identity "IT-Support"
```

These checks help me confirm account state and group membership before making changes.

## Create a Lab User

Example lab command:

```powershell
New-ADUser `
  -Name "Test User" `
  -GivenName "Test" `
  -Surname "User" `
  -SamAccountName "testuser" `
  -UserPrincipalName "testuser@example.local" `
  -Enabled $true `
  -AccountPassword (Read-Host -AsSecureString "Temporary password")
```

## Add the User to a Group

```powershell
Add-ADGroupMember -Identity "IT-Support" -Members "testuser"
```

Verification:

```powershell
Get-ADPrincipalGroupMembership testuser | Select-Object Name
```

## Password Support

```powershell
Set-ADAccountPassword -Identity "testuser" -Reset -NewPassword (Read-Host -AsSecureString "New password")
Unlock-ADAccount -Identity "testuser"
```

I would verify the user's identity and follow the organization's password-reset policy before performing this action.

## Offboarding Workflow

A basic offboarding flow I understand is:

1. Confirm the authorized offboarding request.
2. Disable the account.
3. Remove or review access according to policy.
4. Recover assigned hardware.
5. Record the device condition and accessories.
6. Coordinate data/access handling according to company policy.
7. Update the ticket and asset record.

Example lab command:

```powershell
Disable-ADAccount -Identity "testuser"
```

Verification:

```powershell
Get-ADUser -Identity testuser -Properties Enabled | Select-Object SamAccountName,Enabled
```

## What This Demonstrates

- Active Directory fundamentals
- User/group administration
- Password reset and account status checks
- Identity and access control
- Onboarding/offboarding thinking
- Verification before closing a support request

> Lab note: Production account changes require authorization and company procedures.
