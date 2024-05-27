# Disk Usage Check Script

This shell script monitors disk usage on a Unix-like system and provides alerts when the disk usage exceeds a specified threshold.

```
#!/bin/bash

# Define threshold percentage for alerting (e.g., 80%)
THRESHOLD=80

# Get the disk usage information
df -h | grep -vE '^Filesystem|tmpfs|cdrom' | awk '{print $5 " " $1}' | while read -r line; do
  # Extract the usage percentage and mount point
  usage=$(echo $line | awk '{print $1}' | sed 's/%//')
  mount_point=$(echo $line | awk '{print $2}')

  # Report usage for each filesystem
  echo "Disk usage on $mount_point: $usage%"

  # Check if the usage exceeds the threshold
  if [ "$usage" -gt "$THRESHOLD" ]; then
    echo "Alert: Disk usage on $mount_point has exceeded $THRESHOLD% (currently at $usage%)"
  fi
done

```
