# Lab 09 — Bash Scripting and Automation

## Objective

Write a Bash script that reports the hostname, uptime, memory, root
filesystem usage, and failed systemd units.

## Report script

Save this as `server-report.sh`.

```bash
#!/usr/bin/env bash

set -euo pipefail

printf 'Report time: %s\n' "$(date --iso-8601=seconds)"
printf 'Hostname: %s\n' "$(hostname)"

printf '\nUptime\n'
uptime

printf '\nMemory\n'
free -h

printf '\nRoot filesystem\n'
df -hT /

printf '\nFailed systemd units\n'
systemctl --failed --no-pager
```

## Verify

Run from the directory containing the script.

```bash
bash -n server-report.sh
chmod +x server-report.sh
./server-report.sh
```

The syntax check should exit successfully. The script should print all
four report sections. Install it as root for use by Lab 10.

```bash
install -m 0755 server-report.sh /usr/local/bin/server-report
```

Verification on the VM is pending.
