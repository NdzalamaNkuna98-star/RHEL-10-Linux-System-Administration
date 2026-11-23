# Lab 03 — File Permissions and ACLs

## Objective

Give `labalice` read and write access to a report, give `labbob` read-only
access, and block other ordinary users.

## Configuration

Run as root. This lab uses the accounts from Lab 02.

```bash
mkdir -p /exam/secure
touch /exam/secure/report.txt
chmod 700 /exam/secure
chmod 600 /exam/secure/report.txt
setfacl -m u:labalice:--x,u:labbob:--x /exam/secure
setfacl -m u:labalice:rw-,u:labbob:r-- /exam/secure/report.txt
getfacl -p /exam/secure /exam/secure/report.txt
```

Both users received directory traversal permission, which lets them reach
the report by its full path. The report has a separate ACL for file access.

## Verified ACLs

| Path | `labalice` | `labbob` | Owning group | Others | Mask |
| --- | --- | --- | --- | --- | --- |
| `/exam/secure` | `--x` | `--x` | `---` | `---` | `--x` |
| `/exam/secure/report.txt` | `rw-` | `r--` | `---` | `---` | `rw-` |

## Access tests

```bash
su - labalice -c 'echo "ACL test by Alice" >> /exam/secure/report.txt && cat /exam/secure/report.txt'
su - labbob -c 'cat /exam/secure/report.txt'
su - labbob -c 'echo "Bob write test" >> /exam/secure/report.txt'
runuser -u nobody -- cat /exam/secure/report.txt
```

Expected results are a successful write and read for Alice, a successful
read for Bob, and `Permission denied` for the last two commands. The ACL
configuration was verified with `getfacl`. The user access tests are
pending verification.
