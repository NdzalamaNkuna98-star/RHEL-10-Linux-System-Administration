# Lab 10 — systemd Services and Timers

## Objective

Use a systemd timer to run the Lab 09 server report automatically and
inspect its output in the journal.

## Create the service

Save as `/etc/systemd/system/lab-server-report.service`.

```ini
[Unit]
Description=Generate a server inspection report

[Service]
Type=oneshot
ExecStart=/usr/local/bin/server-report
```

## Create the timer

Save as `/etc/systemd/system/lab-server-report.timer`.

```ini
[Unit]
Description=Run the server inspection report periodically

[Timer]
OnBootSec=2min
OnUnitActiveSec=15min

[Install]
WantedBy=timers.target
```

The timer targets `lab-server-report.service` because the unit names
share the same base name. The first run is scheduled two minutes after
boot. Subsequent runs are scheduled 15 minutes after the service was
last activated.

## Enable and verify

Run as root after installing the script from Lab 09.

```bash
systemctl daemon-reload
systemctl start lab-server-report.service
journalctl -u lab-server-report.service -n 30 --no-pager
systemctl enable --now lab-server-report.timer
systemctl list-timers --all lab-server-report.timer
```

The journal should contain the server report from the manual service
run. After a scheduled trigger, check the journal again to confirm that
the timer started the service automatically. Verification on the VM
is pending.
