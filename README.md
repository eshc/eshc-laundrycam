# eshc-laundrycam
Was previously a cron, python & bash script. Now using systemd.

## Setup

1. On the pi, copy over `laundrycam.service` and `laundrycam.timer` into their correct places.
2. On the pi, edit .ssh/config and add a host for fileserver. Like below:
```
Host fileserver
  user laundrycam
  HostName 10.x.x.x
```
3. On the fileserver, `useradd laundrycam`
4. On the pi, upload the SSH private key or generate a new pair with `ssh-keygen`
5. On the fileserver, edit the `.ssh/authorized_keys` for the laundrycam user, like below:
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINyPtsnO+/mohi2qJaxzG4hKWMO45CVbcHiocSx7aQnV command="/usr/bin/rsync",no-port-forwarding,no-X11-forwarding,no-agent-forwarding,no-pty eshc@laundrycam
```
6. On pi, `sudo systemctl enable --now laundrycam.timer`
7. On pi, after a few seconds, `sudo systemctl status laundrycam` and check no errors.
