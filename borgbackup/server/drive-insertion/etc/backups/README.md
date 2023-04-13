Reference: https://borgbackup.readthedocs.io/en/stable/deployment/automated-local.html

ln -s /etc/backups/40-backup.rules /etc/udev/rules.d/40-backup.rules
ln -s /etc/backups/automatic-backup.service /etc/systemd/system/automatic-backup.service
systemctl daemon-reload
udevadm control --reload

To get the UUID of the disk:
lsblk -o+uuid,label

Borg repo initialization:
borg init --encryption ... /mnt/backup/borg-backups/backup.borg

Start first backup:
systemctl start --no-block automatic-backup

Journal logs:
journalctl -fu automatic-backup [-n number-of-lines]
