# System Uptime Check Script

This script checks the system uptime and displays it in a human-readable format. It utilizes the uptime -p command to retrieve the system uptime information.

### Set Permissions for the Script
Make the script executable:
```
chmod +x uptime_check.sh
```

## Script: uptime_check.sh
```
#!/bin/bash

# Get system uptime in a human-readable format
uptime_info=$(uptime -p)

# Print system uptime
echo "System Uptime:"
echo "$uptime_info"
```
This output displays the system uptime in a concise and human-readable format, showing the total time the system has been up.
