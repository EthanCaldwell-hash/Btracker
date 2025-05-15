# Source Code Directory

This directory contains the core source code for the Btracker application.

## Directory Structure

- `api/`: REST API implementations
- `models/`: Data models and database schemas
- `services/`: Business logic and service implementations
- `utils/`: Utility functions and helper modules

## API Documentation

Detailed API documentation can be found in the `api/` directory. Key endpoints include:

### Token Indexing API

- `POST /api/v1/tokens/index`
- `GET /api/v1/tokens/search`
- `GET /api/v1/tokens/{token_id}`

### Market Data API

- `GET /api/v1/market/price`
- `GET /api/v1/market/volume`
- `GET /api/v1/market/trades`

### User API

- `POST /api/v1/users/register`
- `POST /api/v1/users/login`
- `GET /api/v1/users/profile`

## Development Guidelines

1. Follow REST API best practices
2. Implement proper error handling
3. Add comprehensive API documentation
4. Include unit tests for all endpoints
5. Follow security best practices