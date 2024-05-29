# HTTP Response Times Measurement Script
This script iterates over each URL specified in the URLS array, sends a single HTTP request to each URL, and measures the response time. It then prints the response time for each URL.

### Set Permissions for the Script
Make the script executable:
```
chmod +x http_response_times.sh
```
## Script: http_response_times.sh
```
#!/bin/bash

# URLs to measure response time
URLS=("https://example.com" "https://example2.com")

echo "Measuring HTTP response times..."

# Loop through each URL
for URL in "${URLS[@]}"; do
    echo "URL: $URL"
    
    # Measure response time using curl
    response_time=$(curl -s -o /dev/null -w "%{time_total}\n" "$URL")
    
    # Print response time
    echo "Response time for $URL: $response_time seconds"
done
```
