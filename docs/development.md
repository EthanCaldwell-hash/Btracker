# Btracker Development Guide

This guide provides detailed instructions for setting up and developing the Btracker project.

## Development Environment Setup

### Prerequisites

1. **Required Software**
   - Node.js (>= 16.0.0)
   - Rust (>= 1.65.0)
   - Docker & Docker Compose
   - Solana CLI Tools
   - Git

2. **Recommended IDEs**
   - VS Code with extensions:
     - rust-analyzer
     - Solidity
     - ESLint
     - Prettier

### Initial Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/btracker.git
   cd btracker
   ```

2. **Install Dependencies**
   ```bash
   # Install Solana tools
   sh -c "$(curl -sSfL https://release.solana.com/v1.14.0/install)"

   # Install Rust
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

   # Install frontend dependencies
   cd frontend
   npm install

   # Install backend dependencies
   cd ../backend
   cargo build
   ```

3. **Environment Configuration**
   ```bash
   # Copy environment templates
   cp .env.example .env
   ```

   Edit `.env` with your configuration:
   ```env
   # Solana Configuration
   SOLANA_RPC_URL=http://localhost:8899
   BELIEVE_PROGRAM_ID=your_program_id

   # Database Configuration
   ELASTICSEARCH_URL=http://localhost:9200
   REDIS_URL=redis://localhost:6379

   # X API Configuration
   X_API_KEY=your_x_api_key
   X_API_SECRET=your_x_api_secret

   # Development Settings
   NODE_ENV=development
   PORT=3000
   ```

## Project Structure

```
btracker/
├── backend/
│   ├── src/
│   │   ├── data_collection/    # Solana and X API integration
│   │   ├── processing/         # Data processing logic
│   │   ├── api/               # REST API endpoints
│   │   └── websocket/         # WebSocket server
│   ├── Cargo.toml
│   └── tests/
├── frontend/
│   ├── src/
│   │   ├── components/        # React components
│   │   ├── services/          # API integration
│   │   ├── store/             # Redux store
│   │   └── utils/             # Helper functions
│   ├── package.json
│   └── tests/
└── docs/                      # Documentation
```

## Development Workflow

### 1. Starting Development Environment

```bash
# Start supporting services
docker-compose up -d

# Terminal 1: Start backend
cd backend
cargo run

# Terminal 2: Start frontend
cd frontend
npm run dev
```

### 2. Development Guidelines

#### Code Style

- **Rust**
  - Follow Rust style guide
  - Use `cargo fmt` for formatting
  - Run `cargo clippy` for linting

- **TypeScript/React**
  - Follow Airbnb style guide
  - Use ESLint and Prettier
  - Run `npm run lint` before commits

#### Git Workflow

1. Create feature branch:
   ```bash
   git checkout -b feature/your-feature
   ```

2. Make changes and commit:
   ```bash
   git add .
   git commit -m "feat: add your feature"
   ```

3. Push changes:
   ```bash
   git push origin feature/your-feature
   ```

4. Create pull request on GitHub

### 3. Testing

#### Backend Testing

```bash
cd backend

# Run unit tests
cargo test

# Run specific test
cargo test test_name

# Run with logging
RUST_LOG=debug cargo test
```

#### Frontend Testing

```bash
cd frontend

# Run unit tests
npm test

# Run with coverage
npm test -- --coverage

# Run specific test file
npm test -- ComponentName.test.tsx
```

### 4. Debugging

#### Backend Debugging

1. Using `rust-lldb`:
   ```bash
   rust-lldb target/debug/btracker
   ```

2. Using VS Code:
   - Install CodeLLDB extension
   - Add launch configuration in `.vscode/launch.json`

#### Frontend Debugging

1. Browser DevTools
   - React Developer Tools
   - Redux DevTools

2. VS Code Debugger:
   - Use Chrome Debugger extension
   - Add launch configuration

## API Development

### Adding New Endpoints

1. Create new route module:
   ```rust
   // backend/src/api/routes/token_route.rs
   use actix_web::{get, web, HttpResponse};

   #[get("/tokens/{ticker}")]
   async fn get_token(ticker: web::Path<String>) -> HttpResponse {
       // Implementation
   }
   ```

2. Register route:
   ```rust
   // backend/src/api/mod.rs
   pub fn configure(cfg: &mut web::ServiceConfig) {
       cfg.service(get_token);
   }
   ```

### WebSocket Development

1. Add new message handler:
   ```rust
   // backend/src/websocket/handler.rs
   pub async fn handle_message(msg: Message) -> Result<Message> {
       match msg {
           Message::Text(text) => {
               // Handle text message
           }
           _ => Ok(Message::Close(None))
       }
   }
   ```

## Frontend Development

### Adding New Components

1. Create component:
   ```typescript
   // frontend/src/components/TokenCard.tsx
   import React from 'react';

   interface TokenCardProps {
     ticker: string;
     price: number;
   }

   export const TokenCard: React.FC<TokenCardProps> = ({ ticker, price }) => {
     return (
       <div className="token-card">
         <h3>{ticker}</h3>
         <p>{price}</p>
       </div>
     );
   };
   ```

2. Add styles:
   ```scss
   // frontend/src/styles/components/TokenCard.scss
   .token-card {
     padding: 1rem;
     border-radius: 8px;
     // Add styles
   }
   ```

### State Management

1. Add new Redux slice:
   ```typescript
   // frontend/src/store/slices/tokenSlice.ts
   import { createSlice } from '@reduxjs/toolkit';

   const tokenSlice = createSlice({
     name: 'tokens',
     initialState: [],
     reducers: {
       // Add reducers
     }
   });
   ```

## Performance Optimization

### Backend Optimization

1. Database indexing
2. Caching strategies
3. Connection pooling
4. Query optimization

### Frontend Optimization

1. Code splitting
2. Lazy loading
3. Memoization
4. Bundle optimization

## Troubleshooting

### Common Issues

1. **WebSocket Connection Issues**
   - Check network connectivity
   - Verify WebSocket URL
   - Check server logs

2. **Database Connection Issues**
   - Verify credentials
   - Check service status
   - Review connection logs

### Logging

1. Backend logging:
   ```bash
   RUST_LOG=debug cargo run
   ```

2. Frontend logging:
   ```javascript
   console.log('Debug info:', data);
   ```

## Deployment

### Local Testing

```bash
# Build for production
cd frontend
npm run build

cd ../backend
cargo build --release

# Test production build
docker-compose -f docker-compose.prod.yml up
```

## Additional Resources

- [Rust Documentation](https://doc.rust-lang.org/book/)
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [Solana Documentation](https://docs.solana.com/)
- [Project Wiki](https://github.com/your-username/btracker/wiki)

## Support

For development support:
- Join our [Discord](https://discord.gg/btracker)
- Check our [GitHub Issues](https://github.com/your-username/btracker/issues)
- Email: dev@btracker.io