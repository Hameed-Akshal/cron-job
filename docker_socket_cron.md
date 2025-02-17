# **Configuring Cron to Modify Docker Socket Permissions on Reboot**

## **1. Installing Cron**

### To ensure the cron service is available, install `cronie` on Amazon Linux 2:   
    sudo yum install cronie -y

## **2. Editing the Crontab**

Open the crontab for the current user: 

    crontab -e
Add the following line at the end of the file to modify Docker socket permissions on reboot: 
    
    @reboot sudo chmod 666 /var/run/docker.sock

## **3. Allowing `chmod` Without a Password Prompt**

By default, `sudo` requires a password, which prevents automated execution in a cron job. To bypass this for the `chmod` command:
1) Open the sudoers file:
   
       sudo visudo

2) Add the following line at the end of the file, replacing `<username>` with your actual username:

       <username> ALL=(ALL) NOPASSWD: /bin/chmod 666 /var/run/docker.sock

## **4. Verifying the Configuration**

After rebooting the system, verify the permissions of the Docker socket using:  

    ls -l /var/run/docker.sock
  It should show:   
    
    srw-rw-rw- 1 root docker 0 Feb 12 10:00 /var/run/docker.sock

## **⚠️ Security Considerations**

- Setting `chmod 666` on `/var/run/docker.sock` allows any user to interact with Docker, posing a security risk.
- Consider using the Docker group (`docker`) instead of granting full permissions.

💡 _For security best practices, use `sudo usermod -aG docker <username>` instead of modifying permissions._ 🚀

#

##
