# Scripts Directory

This directory contains utility scripts and tools for the Btracker application.

## Available Scripts

### Development Scripts

```bash
# Start development environment
./dev-setup.sh

# Run database migrations
./migrate.sh

# Generate API documentation
./generate-docs.sh
```

### Deployment Scripts

```bash
# Deploy to production
./deploy.sh

# Backup database
./backup-db.sh

# Restore database
./restore-db.sh
```

### Maintenance Scripts

```bash
# Clean old logs
./clean-logs.sh

# Monitor system resources
./monitor.sh

# Health check
./health-check.sh
```

## Script Guidelines

1. All scripts should be executable (`chmod +x script.sh`)
2. Include proper error handling
3. Add logging for important operations
4. Provide help/usage information
5. Follow shell scripting best practices

## Example Script

```bash
#!/bin/bash

# health-check.sh
# Script to check the health of various system components

check_api() {
    curl -s http://localhost:8000/health
}

check_database() {
    psql -h localhost -U btracker -c "SELECT 1"
}

check_elasticsearch() {
    curl -s http://localhost:9200/_cluster/health
}

main() {
    echo "Checking system health..."
    
    echo "API Status:"
    check_api
    
    echo "Database Status:"
    check_database
    
    echo "Elasticsearch Status:"
    check_elasticsearch
}

main
```

## Automation

Many of these scripts can be automated using cron jobs:

```bash
# Example cron entries

# Run health check every 5 minutes
*/5 * * * * /path/to/scripts/health-check.sh

# Backup database daily at 2 AM
0 2 * * * /path/to/scripts/backup-db.sh

# Clean logs weekly
0 0 * * 0 /path/to/scripts/clean-logs.sh
```