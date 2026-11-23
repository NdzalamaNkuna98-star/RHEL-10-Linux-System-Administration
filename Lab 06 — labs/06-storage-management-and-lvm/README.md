# Lab 06 — Storage Management and LVM

## Objective

Create an LVM logical volume on a dedicated lab disk, format it as XFS,
and configure a persistent mount at `/srv/labdata`.

## Identify the new disk

Attach a blank secondary disk of at least 4 GiB in VirtualBox. Run the
following in the RHEL VM as root.

```bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINTS
```

The commands below assume the new blank disk is `/dev/sdb`. Confirm the
device before running `pvcreate`. These commands initialize storage
and must point to the dedicated blank disk.

## Configure LVM and mount the filesystem

```bash
pvcreate /dev/sdb
vgcreate vg_labdata /dev/sdb
lvcreate -L 2G -n lv_labdata vg_labdata
mkfs.xfs /dev/vg_labdata/lv_labdata
mkdir -p /srv/labdata
blkid -s UUID -o value /dev/vg_labdata/lv_labdata
```

Add this line to `/etc/fstab`, replacing `<FILESYSTEM_UUID>` with the
UUID returned by `blkid`.

```fstab
UUID=<FILESYSTEM_UUID> /srv/labdata xfs defaults 0 0
```

## Verify

```bash
systemctl daemon-reload
findmnt --verify
mount /srv/labdata
findmnt /srv/labdata
df -hT /srv/labdata
pvs
vgs
lvs
```

Expected result is an XFS mount at `/srv/labdata` backed by `lv_labdata`.
Reboot after verification succeeds, then rerun `findmnt /srv/labdata`
to confirm persistence. Verification on the VM is pending.
