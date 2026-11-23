# Lab 05 — Password Aging Policies

## Objective

Configure password aging for the local `labbob` account.

## Configuration and verification

Run as root in the RHEL VM.

```bash
chage -l labbob
chage -m 1 -M 90 -W 14 -I 7 labbob
chage -l labbob
```

| Setting | Value |
| --- | --- |
| Minimum time between password changes | 1 day |
| Maximum password age | 90 days |
| Warning before password expiration | 14 days |
| Inactivity period after password expiration | 7 days |

If the account has no password, use `passwd labbob` to set a lab password
interactively and rerun `chage -l labbob`. Check that the inactivity date
is seven days after the password expiration date.

Verification on the VM is pending.
