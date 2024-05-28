# Network Connectivity Check Script

This script checks the network connectivity to a specified host (google.com) and logs the results to a file (output.txt). It is useful for monitoring the reachability of a critical external service or website.
### Prerequisites
Create the Output.txt and give permissions
```
touch /path/to/output.txt
chmod 666 /path/to/output.txt
```
### Set Permissions for the Script
Make the script executable:
```
chmod +x check_network_connectivity.sh
```
# Script for Network Connectivity
check_network_connectivity.sh
```
#!/bin/bash

# Host to check
HOST="google.com"

# Log file for results
LOG_FILE="/path/to/output.txt"

# To check network connectivity and log the result
if ping -c 4 "$HOST" &> /dev/null; then
    echo "$(date): Host $HOST is reachable." >> "$LOG_FILE"
  else
    echo "$(date): Host $HOST is not reachable!" >> "$LOG_FILE"
  fi
```
#### This README provides a comprehensive guide to installing, configuring, and using the network connectivity check script.
