# Database Backup Script

This script performs a backup of a specified MySQL database and saves the backup file to a specified directory. It uses the mysqldump command to create the backup and assumes the MySQL root password is set up using native password authentication.

### Prerequisites
- MySQL server installation
```
sudo apt-get install mysql-client
```
- Setting Up MySQL Root Password
1. Open a terminal and log into MySQL as the root user:
```
mysql -u root -p
```
2. Inside the MySQL shell, run the following commands to set the root password:
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
FLUSH PRIVILEGES;
```
## Steps to Set Up and Run the Script
### 1. Create the Backup Directory:
 Ensure the directory where backups will be stored exists. The script will create it if it does not:
```
mkdir -p /path/to/backup/directory
```
### 2. Set Permissions for the Script
Make the script executable:
```
chmod +x database_backup.sh
```
## Script: database_backup.sh
```
#!/bin/bash

# Database credentials
DB_NAME="your_db_name"

# Backup directory
BACKUP_DIR="/path/to/backup/directory"

# Date format for the backup file
DATE=$(date +'%Y-%m-%d_%H-%M-%S')

# Backup file name
BACKUP_FILE="$BACKUP_DIR/$DB_NAME-$DATE.sql"

# Create the backup directory if it doesn't exist
mkdir -p "$BACKUP_DIR"

# Perform the database backup
echo "$(date): Starting database backup for $DB_NAME"
mysqldump -u root -p "$DB_NAME" > "$BACKUP_FILE"
echo "$(date): Database backup completed. Backup file: $BACKUP_FILE"
```
By following these steps and using the provided script, you can create regular backups of your MySQL database and ensure that your data is safely stored.
