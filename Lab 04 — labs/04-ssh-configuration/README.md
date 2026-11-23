# Lab 04 — SSH Configuration

## Objective

Set up SSH public-key authentication for `labalice` and verify a local
connection to the RHEL VM.

## Start the SSH server

Run as root. Install `openssh-server` with `dnf` if the service is missing.

```bash
systemctl enable --now sshd
systemctl is-active sshd
su - labalice
```

## Create and authorize a key

Run as `labalice`. Use the dedicated key filename below on the first run.
If the key already exists, skip key generation.

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_lab04 -C "labalice-ssh-lab"
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
grep -qxF -f ~/.ssh/id_ed25519_lab04.pub ~/.ssh/authorized_keys || cat ~/.ssh/id_ed25519_lab04.pub >> ~/.ssh/authorized_keys
```

Keep the private key in the VM. `authorized_keys` contains the public key.

## Verify key-based login

```bash
ssh -o PreferredAuthentications=publickey -o IdentitiesOnly=yes -i ~/.ssh/id_ed25519_lab04 labalice@localhost whoami
```

Expected output is `labalice`. If the key has a passphrase, SSH may ask for
it to unlock the private key. Verification on the VM is pending.
