# System Monitoring Script
This script monitors system processes and memory usage using the ps aux and free commands. It displays detailed information about all running processes, highlights the top processes by CPU and memory usage, and provides a summary of the system's memory usage.

### Set Permissions for the Script
Make the script executable:
```
chmod +x monitor_system.sh
```

### Script: monitor_system.sh
```
#!/bin/bash

# Print the current date and time
echo "System Monitoring Report - $(date)"
echo

# Print all processes using ps aux
echo "All Processes:"
ps aux
echo

# Print top 10 processes by CPU usage
echo "Top 10 Processes by CPU Usage:"
ps aux --sort=-%cpu | head -n 10
echo

# Print top 10 processes by memory usage
echo "Top 10 Processes by Memory Usage:"
ps aux --sort=-%mem | head -n 10
echo

# Print memory usage
echo "Memory Usage:"
free -h
echo

# Print a message indicating that the monitoring report is complete
echo "System monitoring report generated successfully."
```
