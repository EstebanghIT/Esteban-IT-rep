# 05 — IT Asset, Onboarding & Security Workflow

## Purpose

This project documents how I would organize common internal IT operational tasks. It is a workflow exercise aligned with IT support responsibilities; it is **not a claim that I have administered Odoo in production**.

## Asset Record

For each workstation I would keep fields such as:

```text
Asset ID
Serial number
Manufacturer / model
CPU / RAM / storage
Operating system
Assigned user
Department
Location
Purchase / deployment date
Warranty status
Device condition
Last maintenance date
Next maintenance date
Accessories
Lifecycle status
Notes
```

This structure can be transferred to an IT asset-management platform such as Odoo when the organization uses it.

## New Hire — Technical Onboarding

```text
[ ] Confirm authorized onboarding request
[ ] Identify required workstation/configuration
[ ] Record asset and serial number
[ ] Prepare operating system
[ ] Apply required updates
[ ] Verify drivers
[ ] Verify antivirus/security controls
[ ] Install approved software
[ ] Create/verify authorized account access
[ ] Test network/VPN if required
[ ] Test peripherals
[ ] Record equipment assigned to employee
[ ] Confirm delivery/receipt
[ ] Update support/asset records
```

## Offboarding

```text
[ ] Confirm authorized offboarding request
[ ] Disable/review account access according to policy
[ ] Recover workstation and peripherals
[ ] Confirm serial/asset ID
[ ] Inspect device condition
[ ] Record missing/damaged equipment
[ ] Handle data according to company policy
[ ] Update asset status
[ ] Decide whether device is reusable, requires repair, or has reached EOL
```

## Patch & Security Workflow

Before applying changes in a production environment I would follow approved documentation and change procedures.

```text
1. Identify affected endpoint(s)
2. Check current OS/update status
3. Review approved patch/change
4. Confirm backup/recovery requirements
5. Apply according to company procedure
6. Restart if required
7. Verify endpoint functionality
8. Verify security protection
9. Document result/failure
10. Escalate when necessary
```

Useful Windows checks from the endpoint-support project include:

```powershell
systeminfo
Get-HotFix | Sort-Object InstalledOn -Descending
Get-MpComputerStatus
Get-PnpDevice | Where-Object {$_.Status -ne "OK"}
```

## Software Licensing Audit Concept

A licensing audit should compare installed/assigned software against the organization's authorized license records. I would document exceptions rather than purchasing or changing licensing without authorization.

For Microsoft 365, my current experience is at the fundamentals/lab level for account and license administration.

## EOL Decision Factors

I would document factors such as:

- Hardware age and warranty
- Reliability/failure history
- Performance against required applications
- Upgrade feasibility
- Security/OS support status
- Repair cost versus replacement
- Reusable components
- Approved disposal/reuse process

## What This Demonstrates

Organization, asset-management thinking, onboarding/offboarding, endpoint security awareness, lifecycle planning and documentation.

> This page intentionally distinguishes workflow knowledge from professional Odoo/enterprise asset-management experience.
