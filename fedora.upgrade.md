
Backup your data on Fedora 29. Do not skip this step. This author is not liable for any data loss.
Patch and update Fedora 29, run:
```bash
sudo dnf --refresh upgrade
sudo dnf install dnf-plugin-system-upgrade
sudo dnf system-upgrade download --releasever=30
sudo dnf system-upgrade reboot
```
Install or update dnf-plugin-system-upgrade package on Fedora 29: sudo dnf install dnf-plugin-system-upgrade
Start upgrading F29 to F30, execute: sudo dnf system-upgrade download --releasever=30
Upgrade 29 to Fedora 30 by rebooting the system: sudo dnf system-upgrade reboot
