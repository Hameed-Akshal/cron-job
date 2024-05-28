# Service Health Check Script

This shell script monitors the health of specified services on a Unix-like system and provides alerts if any service is not running.
```
#!/bin/bash

# List of services to check
service="ssh"

if systemctl is-active --quiet "$service"; then
      echo "Service $service is running."
    else
      echo "Service $service is not running!"
    fi
```
