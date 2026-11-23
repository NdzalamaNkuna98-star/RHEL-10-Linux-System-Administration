# Lab 07 — Network Configuration

## Objective

Use NetworkManager to configure a static IPv4 address on a secondary
lab interface while keeping the primary NAT connection available.

## Identify the interface

Attach a second VirtualBox network adapter on a host-only network.
Run these commands as root from the VM console.

```bash
nmcli device status
nmcli connection show
ip -br address
ip route
```

This example assumes the secondary NIC is `enp0s8` and the host-only
network uses `192.168.56.0/24`. Verify the interface and choose an
unused address in your host-only subnet before applying the example.

## Configure the connection

```bash
nmcli connection add type ethernet ifname enp0s8 con-name lab-static ipv4.method manual ipv4.addresses 192.168.56.20/24 ipv4.never-default yes ipv6.method disabled
nmcli connection up lab-static
```

## Verify

```bash
nmcli connection show --active
ip -br address show enp0s8
ip route
```

The secondary interface should have `192.168.56.20/24`. The existing
default route should still use the primary NAT interface. From another
system on the same host-only network, test reachability to the new IP.

Verification on the VM is pending.
