# Btracker API Documentation

This document outlines the API endpoints and usage for the Btracker platform.

## Base URL

```
https://api.btracker.io/v1
```

## Authentication

All API requests require an API key passed in the header:

```
Authorization: Bearer YOUR_API_KEY
```

## Endpoints

### Token Indexing

#### Get Latest Tokens

```http
GET /tokens/latest
```

Retrieve the most recently launched tokens.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| limit | integer | Number of tokens to return (default: 50, max: 100) |
| offset | integer | Pagination offset (default: 0) |

**Response:**

```json
{
  "tokens": [
    {
      "name": "NUGGS",
      "ticker": "$NUGGS",
      "launch_time": "2025-05-01T09:00:00Z",
      "initial_price": "0.015",
      "current_price": "0.075",
      "liquidity_pool": "6000",
      "anti_snipe_fee": "9",
      "market_cap": "1000000",
      "description": "Decentralized food delivery platform"
    }
  ],
  "total": 100,
  "offset": 0
}
```

#### Get Token Details

```http
GET /tokens/{ticker}
```

Retrieve detailed information about a specific token.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| ticker | string | Token ticker symbol (e.g., $NUGGS) |

**Response:**

```json
{
  "name": "NUGGS",
  "ticker": "$NUGGS",
  "launch_time": "2025-05-01T09:00:00Z",
  "initial_price": "0.015",
  "current_price": "0.075",
  "liquidity_pool": "6000",
  "anti_snipe_fee": "9",
  "market_cap": "1000000",
  "description": "Decentralized food delivery platform",
  "x_post": {
    "id": "123456789",
    "content": "@launchcoin $NUGGS Nugget - A decentralized food delivery platform",
    "author": "@founder",
    "timestamp": "2025-05-01T08:59:00Z"
  },
  "price_history": [
    {
      "timestamp": "2025-05-01T09:00:00Z",
      "price": "0.015"
    },
    {
      "timestamp": "2025-05-01T09:01:00Z",
      "price": "0.045"
    }
  ]
}
```

### Real-Time Updates

#### WebSocket Connection

```
wss://api.btracker.io/v1/ws
```

Connect to receive real-time token updates.

**Connection Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| api_key | string | Your API key |

**Message Types:**

1. New Token Launch:
```json
{
  "type": "new_token",
  "data": {
    "name": "NUGGS",
    "ticker": "$NUGGS",
    "launch_time": "2025-05-01T09:00:00Z",
    "initial_price": "0.015"
  }
}
```

2. Price Update:
```json
{
  "type": "price_update",
  "data": {
    "ticker": "$NUGGS",
    "price": "0.075",
    "timestamp": "2025-05-01T09:01:00Z"
  }
}
```

3. Risk Alert:
```json
{
  "type": "risk_alert",
  "data": {
    "ticker": "$NUGGS",
    "risk_level": "high",
    "reason": "Anomalous sell orders detected",
    "timestamp": "2025-05-01T09:02:00Z"
  }
}
```

### Analytics

#### Get Market Statistics

```http
GET /analytics/market
```

Retrieve overall market statistics.

**Response:**

```json
{
  "total_tokens": 1000,
  "daily_launches": 50,
  "total_volume_24h": "1000000",
  "average_initial_price": "0.025",
  "average_anti_snipe_fee": "8.5"
}
```

## Rate Limits

- REST API: 100 requests per minute
- WebSocket: 1 connection per API key

## Error Codes

| Code | Description |
|------|-------------|
| 401 | Unauthorized - Invalid API key |
| 404 | Resource not found |
| 429 | Rate limit exceeded |
| 500 | Internal server error |

## SDK Examples

### JavaScript

```javascript
const Btracker = require('btracker-sdk');

const client = new Btracker('YOUR_API_KEY');

// Get latest tokens
client.getLatestTokens().then(tokens => {
  console.log(tokens);
});

// Subscribe to real-time updates
client.subscribe('new_token', token => {
  console.log('New token launched:', token);
});
```

### Python

```python
from btracker import BtrackerClient

client = BtrackerClient('YOUR_API_KEY')

# Get latest tokens
tokens = client.get_latest_tokens()
print(tokens)

# Subscribe to real-time updates
def on_new_token(token):
    print(f'New token launched: {token}')

client.subscribe('new_token', on_new_token)
```

## Support

For API support, please contact api@btracker.io or visit our [Developer Forum](https://forum.btracker.io).