# Lab 02 — User and Group Management

## Objective

Create two local accounts with private primary groups and a shared
supplementary group.

## Configuration

Run as root in the RHEL VM.

```bash
groupadd linuxops
useradd -m -U -G linuxops labalice
useradd -m -U -G linuxops labbob
```

`-m` creates a home directory, `-U` creates a private primary group,
and `-G linuxops` assigns the shared supplementary group.

## Verification

```bash
id labalice
id labbob
getent group linuxops
ls -ld /home/labalice /home/labbob
su - labalice -c 'whoami; pwd; id -nG'
su - labbob -c 'whoami; pwd; id -nG'
```

Both users were verified in login shells. Each session started in its
own home directory and included `linuxops` in its groups.

| User | UID | Primary group | Home directory |
| --- | --- | --- | --- |
| `labalice` | 1001 | `labalice` (1002) | `/home/labalice` |
| `labbob` | 1002 | `labbob` (1003) | `/home/labbob` |

Both home directories were owned by their respective users and primary
groups, with mode `700`. The `linuxops` GID was `1001`.

## Troubleshooting

Lowercase `-u` expects a numeric UID. I corrected my initial `useradd`
command by using `-U` for the private group and `-G linuxops` for the
supplementary group.
