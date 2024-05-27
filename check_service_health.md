# Service Health Check Script

This shell script monitors the health of specified services on a Unix-like system and provides alerts if any service is not running.
```
#!/bin/bash

# List of services to check
services=(
  "nginx"
  "ssh"
)

# Email settings
EMAIL="hameed.a@xcelcorp.com"
SUBJECT="Service Health Alert"

if systemctl is-active --quiet "$service"; then
      echo "Service $service is running."
    else
      echo "Service $service is not running!"
      echo "Service $service is not running!" | mail -s "$SUBJECT" "$EMAIL"
    fi
```
