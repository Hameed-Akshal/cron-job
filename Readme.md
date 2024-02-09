## Installing Cron
sudo yum install cronie  # For Amazon Linux 2
## Open the crontab for editing
crontab -e
## Add the following line to the crontab:
@reboot sudo chmod 666 /var/run/docker.sock
## To configure sudo to allow a specific command without a password prompt for your user in the sudoers file
sudo visudo
## Add the following line to the sudoers file, replacing <username> with your actual username:
<username> ALL=(ALL) NOPASSWD: /bin/chmod 666 /var/run/docker.sock
