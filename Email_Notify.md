# Email Notification Script

This repository contains a Bash script for sending email notifications using `ssmtp` and `mutt`. The script can send emails with a subject and body, and it supports attachments when using `mutt`.

## Requirements

- `ssmtp`
- `mutt`

## Installation

### Install `ssmtp` and `mutt`

On a Debian-based system (like Ubuntu), you can install `ssmtp` and `mutt` using the following commands:

```
sudo apt update
sudo apt install ssmtp mutt
```
On a Rhel-based system (like CentOs), you can install `ssmtp` and `mutt` using the following commands:

```
sudo yum update
sudo yum install ssmtp mutt
```

## Configure ssmtp
1. Edit the ssmtp configuration file to set up your email account. Open /etc/ssmtp/ssmtp.conf in your favorite text editor:
```
sudo nano /etc/ssmtp/ssmtp.conf
```
2. Add or modify the following lines with your email account details:
```
root=your_email@example.com
mailhub=smtp.example.com:587
AuthUser=your_email@example.com
AuthPass=your_password
UseTLS=YES
UseSTARTTLS=YES
hostname=your_hostname
```
Replace the placeholders with your actual email credentials and SMTP server details.


## Debian-based like Ubuntu
### Script: email_notify.sh
```
#!/bin/bash

# Email details
TO="recipient@example.com"
FROM="your_email@example.com"
SUBJECT="Notification Subject"
BODY="This is the body of the notification email."
ATTACHMENT="/path/to/attachment.txt"  # Optional attachment

# Send email using mutt
send_email_mutt() {
  if [ -f "$ATTACHMENT" ]; then
    echo "$BODY" | mutt -s "$SUBJECT" -a "$ATTACHMENT" -- $TO
  else
    echo "$BODY" | mutt -s "$SUBJECT" -- $TO
  fi
}

send_email_mutt 

```

### Set Permissions for the Script
Make the script executable:
```
chmod +x email_notify.sh
```
## Security Note

-   Ensure that the email sending credentials are secure. Avoid hardcoding passwords in the script for production use. Consider using environment variables or secure credential storage solutions.


This README provides an overview of the script, instructions for installation, usage, and customization, as well as a security note. Adjust the content as necessary to fit your specific project details and environment.
