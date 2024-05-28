# Automatic Package Updates Script
This script automates the process of updating and cleaning up system packages on a Debian-based system using the apt-get package manager.

### Set Permissions for the Script
Make the script executable:
```
chmod +x automatic_updates.sh
```
## Debian-based like Ubuntu
### Script: automatic_updates.sh
```
#!/bin/bash

# Update package lists
sudo apt-get update

# Perform package upgrades
sudo apt-get upgrade -y

# Perform distribution upgrades (if any)
sudo apt-get dist-upgrade -y

# Clean up unused packages and cached files
sudo apt-get autoclean
sudo apt-get autoremove -y

# Print message
echo "System packages Updated and cleaned Up"
```

## RPM-based like Amazon Liunx, CentOS, RHEL
### Script: automatic_updates.sh
```
#!/bin/bash

# Update package lists
sudo yum update -y

# Clean up cached files
sudo yum clean all

# Print message
echo "System packages Updated and cleaned Up"
```
For Amazon Linux systems, the package manager used is yum or its newer version, dnf. Here's the equivalent script for performing automatic package updates on Amazon Linux using yum
