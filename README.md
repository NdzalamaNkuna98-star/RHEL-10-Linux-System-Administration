# RHEL 10 | Linux System Administration Portfolio

**Hands-on labs in Linux administration, security, networking, and automation**

I built this portfolio to practice administering Red Hat Enterprise Linux
in a virtual lab. Each lab includes the objective, the commands needed to
reproduce the setup, and checks to verify the result.

**Lab environment:** Red Hat Enterprise Linux 10.1 · Oracle VirtualBox · Bash

## Lab Index

| Lab | Topic | Practical outcome |
|:---:|---|---|
| 01 | [Linux Server Inspection](labs/01-linux-server-inspection/README.md) | Establish a server baseline across CPU, memory, storage, networking, and systemd. |
| 02 | [User and Group Management](labs/02-user-and-group-management/README.md) | Create local accounts and verify home ownership, group membership, and login sessions. |
| 03 | [File Permissions and ACLs](labs/03-file-permissions-and-acls/README.md) | Give one user read/write access to a report and another read-only access. |
| 04 | [SSH Configuration](labs/04-ssh-configuration/README.md) | Configure and test SSH public-key authentication for a local user. |
| 05 | [Password Aging Policies](labs/05-password-aging-policies/README.md) | Set password age limits, expiry warnings, and account inactivity rules. |
| 06 | [Storage Management and LVM](labs/06-storage-management-and-lvm/README.md) | Create an XFS filesystem on an LVM logical volume and mount it persistently. |
| 07 | [Network Configuration](labs/07-network-configuration/README.md) | Assign a static IPv4 address to a secondary interface while preserving the default route. |
| 08 | [Firewall and SELinux](labs/08-firewall-and-selinux/README.md) | Serve an Apache test page on a custom port with SELinux enforcing and a firewalld rule. |
| 09 | [Bash Scripting and Automation](labs/09-bash-scripting-and-automation/README.md) | Build a script that reports server health and lists failed systemd units. |
| 10 | [systemd Services and Timers](labs/10-systemd-services-and-timers/README.md) | Schedule the server report and verify its execution in the system journal. |

## Verification Status

- **Labs 01–02** · Completed and verified on the RHEL VM.
- **Lab 03** · Directory and file ACLs verified with `getfacl`. User-level access tests are pending.
- **Labs 04–10** · Procedures and expected outcomes documented. VM verification is pending.
