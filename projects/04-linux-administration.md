# 04 — Linux Administration & Troubleshooting

## Scenario

Prepare a Linux system for a support user, apply group-based permissions, verify a service and diagnose basic connectivity.

## User and Group Administration

```bash
sudo adduser testuser
sudo groupadd support
sudo usermod -aG support testuser
groups testuser
id testuser
```

## File Permissions

```bash
sudo mkdir /srv/support-files
sudo chown root:support /srv/support-files
sudo chmod 770 /srv/support-files
ls -ld /srv/support-files
```

`770` gives full access to the owner and group while preventing access for other users.

## Processes

```bash
ps aux
top
```

For a specific process:

```bash
ps aux | grep ssh
```

## Services

```bash
systemctl status ssh
systemctl is-enabled ssh
```

If an authorized lab requires starting the service:

```bash
sudo systemctl start ssh
```

Then verify again:

```bash
systemctl status ssh
```

## Networking

```bash
ip addr
ip route
ping -c 4 127.0.0.1
ping -c 4 <default-gateway>
ss -tulpn
```

DNS checks:

```bash
getent hosts example.com
```

## Disk and Memory

```bash
df -h
free -h
```

## Troubleshooting Logic

For a connectivity issue I would check interface/IP → route → gateway → DNS → listening service, rather than changing several settings at once.

## What This Demonstrates

Linux CLI, users/groups, permissions, processes, services, resource checks and basic network troubleshooting.
