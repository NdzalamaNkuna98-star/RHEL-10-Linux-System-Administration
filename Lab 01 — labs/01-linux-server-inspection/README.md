# Lab 01 — Linux Server Inspection

## Objective

Establish a baseline for a RHEL 10.1 server running in Oracle VirtualBox.

## Commands

```bash
cat /etc/redhat-release
hostnamectl
uptime
lscpu
free -h
lsblk -f
df -hT /
ip -br address
ip route
systemctl is-system-running
systemctl --failed
```

## Verified results

| Area | Finding |
| --- | --- |
| Operating system | Red Hat Enterprise Linux 10.1 (Coughlan), x86-64 |
| Hostname | The static hostname was unset and the VM used `localhost`. |
| CPU and memory | 1 vCPU, 1.7 GiB of RAM, and 2.0 GiB of swap. No swap was in use. |
| Storage | `/` was XFS on `/dev/mapper/rhel-root`, with 17G total and 26% used. `/boot` was on `/dev/sda2`. |
| Networking | `enp0s3` was up with `10.0.2.15/24` and a DHCP-provided default route via `10.0.2.2`. |
| System health | systemd reported `running` with zero failed units. |

`lsblk -f` showed that `/dev/sda3` backed the LVM logical volume for `/`.
`df -hT /` showed the usable space on the mounted filesystem.
