# 01 — Windows Endpoint Support & Preventive Maintenance

## Scenario

A Windows workstation is reported as slow and the user says applications are taking longer than usual to open. The objective is to diagnose the issue without immediately reinstalling the operating system.

## What I Check First

### 1. System information

```powershell
systeminfo
hostname
whoami
```

I use these commands to confirm the machine, logged-in user and operating-system information before making changes.

### 2. IP and connectivity

```powershell
ipconfig /all
ping 127.0.0.1
ping <default-gateway>
nslookup microsoft.com
```

This separates a local workstation problem from a network or DNS problem.

### 3. Running processes

```powershell
tasklist
```

I also use **Task Manager** to review CPU, memory, disk and startup usage.

### 4. Storage

```powershell
Get-Volume
```

I check whether the system drive is running low on free space because this can affect workstation performance and updates.

### 5. Windows services

```powershell
Get-Service
Get-Service | Where-Object {$_.Status -eq "Stopped"}
```

For a specific service:

```powershell
Get-Service -Name wuauserv
```

### 6. Windows Update

```powershell
Get-HotFix | Sort-Object InstalledOn -Descending
```

I also check **Settings > Windows Update** for pending updates or restart requirements.

### 7. Drivers

```powershell
Get-PnpDevice | Where-Object {$_.Status -ne "OK"}
```

I verify suspicious devices in **Device Manager** before changing a driver.

### 8. Event Viewer

```powershell
eventvwr.msc
```

I review relevant System/Application events around the time the issue occurred instead of assuming every warning is the cause.

### 9. Microsoft Defender

```powershell
Get-MpComputerStatus
```

I check antivirus status and protection state before concluding the machine is healthy.

## Preventive Maintenance Checklist

- Windows updates checked
- Driver/device status checked
- Antivirus protection verified
- Disk space checked
- Startup load reviewed
- Critical applications tested
- Network connectivity verified
- Peripherals checked
- Relevant errors documented
- User confirms normal operation

## Verification

After making a change, I reproduce the original workflow and confirm the issue is actually resolved. I would document what was checked, the change made, the result and any follow-up required.

## Why This Matters for IT Support

This workflow demonstrates workstation maintenance, driver/update awareness, antivirus checks, performance troubleshooting, documentation and preventive maintenance.

> Lab note: Commands should be run only on systems I am authorized to administer.
