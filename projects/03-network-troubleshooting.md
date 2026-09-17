# 03 — Cisco Network Configuration & Troubleshooting

## Scenario

Two user groups are separated into VLANs. A workstation later loses connectivity. The goal is to verify the configuration layer by layer and identify the root cause.

## Example Topology

```text
PC-USER ----\
             SW1 ---- R1
PC-IT ------/
```

- VLAN 10 — USERS
- VLAN 20 — IT

## Switch Configuration

```text
enable
configure terminal

vlan 10
 name USERS
exit

vlan 20
 name IT
exit

interface fastEthernet0/1
 switchport mode access
 switchport access vlan 10
exit

interface fastEthernet0/2
 switchport mode access
 switchport access vlan 20
exit
```

## Verification Commands

```text
show vlan brief
show interfaces status
show running-config
show mac address-table
```

These commands let me confirm VLAN membership, interface state and learned MAC addresses.

## Windows Client Checks

```powershell
ipconfig /all
ping 127.0.0.1
ping <default-gateway>
arp -a
nslookup example.com
tracert example.com
```

## Troubleshooting Example

**Symptom:** PC-USER cannot reach its gateway.

I would check:

```text
show interfaces status
show vlan brief
show running-config interface fastEthernet0/1
```

If Fa0/1 was accidentally placed in VLAN 20, I would correct it:

```text
configure terminal
interface fastEthernet0/1
 switchport mode access
 switchport access vlan 10
end
```

Then verify:

```text
show vlan brief
```

And from the client:

```powershell
ipconfig /all
ping <default-gateway>
```

## DHCP Troubleshooting

On Windows:

```powershell
ipconfig /release
ipconfig /renew
ipconfig /all
```

On Cisco equipment, depending on the lab configuration:

```text
show ip interface brief
show ip route
show ip dhcp binding
show running-config
```

## Troubleshooting Method

1. Confirm physical/interface status.
2. Check client IP configuration.
3. Verify VLAN membership.
4. Test the local gateway.
5. Check routing.
6. Check DHCP/DNS if relevant.
7. Make one controlled change.
8. Retest and document the result.

## What This Demonstrates

TCP/IP, VLANs, DHCP, Cisco IOS, connectivity troubleshooting, fault isolation and verification.
