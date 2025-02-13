# Database Comparison Script

## Overview

This Bash script compares the schema of two PostgreSQL databases hosted on **PostgreSQL** to identify any differences in table structures.


## Prerequisites

Ensure you have the following installed:

- PostgreSQL client (`psql`)

- Bash shell (Linux/macOS or Windows with WSL)


## Configuration

Update the following database connection details in the script:

```
DB1_HOST="dev_db.postgres.database.azure.com"
DB1_PORT="5432"
DB1_NAME="dev_v2"
DB1_USER="postgres"
DB1_PASSWORD="<SENSITIVE_CONTENT>"

DB2_HOST="prod_db.postgres.database.azure.com"
DB2_PORT="5432"
DB2_NAME="prod_v2"
DB2_USER="postgres"
DB2_PASSWORD="<SENSITIVE_CONTENT>"
```

## Usage

### Set Permissions for the Script

 Make the script executable:
```
chmod +x compare_schemas.sh
```
### Run the Script
```
/compare_schemas.sh
```
This will initiate the schema comparison process between the development and production databases.

## How It Works

### Script: compare\_schemas.sh
```
#!/bin/bash

# Export passwords for psql
export PGPASSWORD=$DB1_PASSWORD
DB1_SCHEMA=$(psql -h $DB1_HOST -p $DB1_PORT -U $DB1_USER -d $DB1_NAME -t -c "SELECT table_name, column_name FROM information_schema.columns WHERE table_schema = 'public' ORDER BY table_name, ordinal_position;")

export PGPASSWORD=$DB2_PASSWORD
DB2_SCHEMA=$(psql -h $DB2_HOST -p $DB2_PORT -U $DB2_USER -d $DB2_NAME -t -c "SELECT table_name, column_name FROM information_schema.columns WHERE table_schema = 'public' ORDER BY table_name, ordinal_position;")

# Compare schemas
DIFF=$(diff <(echo "$DB1_SCHEMA") <(echo "$DB2_SCHEMA"))

if [ -z "$DIFF" ]; then
  echo "Databases have the same schema."
else
  echo "Differences between the databases:"
  echo "$DIFF" | while read -r line; do
    if [[ $line == "<"* ]]; then
      echo "- In $DB1_NAME: ${line#< }"
    elif [[ $line == ">"* ]]; then
      echo "- In $DB2_NAME: ${line#> }"
    fi
  done
fi
```
## Expected Output

If the schemas match:

**Databases have the same schema.**

If there are differences:

**Differences between the databases:**

**- In dev\_v2: table\_name column\_name**

**- In prod\_v2: table\_name column\_name**

## Notes

- Ensure that **both databases** allow connections from the machine running the script.

- If `PGPASSWORD` is empty, the script will prompt for a password.

- The script assumes both databases use the `public` schema.

- Make sure the PostgreSQL client (`psql`) is installed and available in your system PATH.

## Troubleshooting

  - If you get a **connection error**, ensure:

  - The database hostnames and credentials are correct.

  - Your IP is allowed in the **Azure PostgreSQL firewall settings**.

- If the script shows `command not found: psql`, install PostgreSQL client:
```
sudo apt install postgresql-client  # Ubuntu/Debian
brew install postgresql  # macOS
```

