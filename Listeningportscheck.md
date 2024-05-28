# Listening Ports Check Script
This script lists the listening ports on the system by utilizing the netstat command and filtering the output with grep.

### Set Permissions for the Script
Make the script executable:
```
chmod +x listening_ports.sh
```
## Script: listening_ports.sh
```
#!/bin/bash

# Get listening ports using netstat and filter with grep
listening_ports=$(netstat -tuln | grep LISTEN)

# Print listening ports
echo "Listening Ports:"
echo "$listening_ports"
```
This output displays the listening ports along with their protocol, local address, and state.
