# Lab 08 — Firewall and SELinux

## Objective

Serve an Apache test page on TCP port 8585 using an SELinux port label
and a firewalld rule for the lab interface.

## Prepare the server

Run as root. Package installation requires access to the RHEL repositories.
Check that port 8585 is free, that SELinux reports `Enforcing`, and that
the port has no conflicting SELinux assignment before adding the label.

```bash
dnf install -y httpd firewalld policycoreutils-python-utils
getenforce
ss -ltn
semanage port -l | grep -w 8585
```

## Configure Apache and SELinux

```bash
printf 'Listen 8585\n' > /etc/httpd/conf.d/lab08-listen.conf
printf 'RHEL 10 firewall and SELinux lab\n' > /var/www/html/lab08.html
restorecon -v /var/www/html/lab08.html
semanage port -a -t http_port_t -p tcp 8585
httpd -t
systemctl enable --now httpd
systemctl restart httpd
```

## Open the port in the lab interface's zone

```bash
systemctl enable --now firewalld
firewall-cmd --get-active-zones
```

Replace `<lab-zone>` with the zone assigned to the interface used by the
test client.

```bash
firewall-cmd --permanent --zone=<lab-zone> --add-port=8585/tcp
firewall-cmd --reload
firewall-cmd --zone=<lab-zone> --query-port=8585/tcp
curl --fail http://127.0.0.1:8585/lab08.html
```

## Verify from a second system

From a system that can reach the VM, run the following with the VM's
reachable IP address.

```bash
curl --fail http://<VM-IP>:8585/lab08.html
```

A successful local request confirms Apache is serving the page. A
successful remote request also verifies that the client can reach it
through the firewall. Verification on the VM is pending.
