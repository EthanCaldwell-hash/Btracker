# Configuration Directory

This directory contains all configuration files for the Btracker application.

## Configuration Files

### Application Configuration

- `app.yaml`: Main application configuration
- `database.yaml`: Database connection settings
- `logging.yaml`: Logging configuration

### Environment Files

- `.env.development`: Development environment variables
- `.env.production`: Production environment variables
- `.env.test`: Test environment variables

## Configuration Guidelines

### Security

1. Never commit sensitive information (API keys, passwords)
2. Use environment variables for sensitive data
3. Implement proper encryption for stored credentials

### Database Configuration

```yaml
# Example database.yaml
database:
  host: localhost
  port: 5432
  name: btracker
  pool:
    max_size: 20
    timeout_seconds: 30
```

### Logging Configuration

```yaml
# Example logging.yaml
logging:
  level: info
  format: json
  output: stdout
  file:
    enabled: true
    path: /var/log/btracker
    rotate:
      max_size: 100MB
      max_files: 5
```

## Environment Variables

Key environment variables used in the application:

```env
# API Configuration
API_PORT=8000
API_HOST=0.0.0.0

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/btracker

# Authentication
JWT_SECRET=your-secret-key
JWT_EXPIRATION=24h

# External Services
SOLANA_RPC_URL=https://api.mainnet-beta.solana.com
ELASTICSEARCH_URL=http://localhost:9200
```