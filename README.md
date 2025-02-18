# Gophermat

Gophermat is a Go-based backend service that provides an API for user authentication, order management, and balance transactions.

## Features
- User registration and authentication
- Order management (uploading and retrieving orders)
- Balance management (retrieving user balance and making withdrawals)
- Middleware support for authentication and logging
- Graceful shutdown handling

## Technologies Used
- Go (Golang)
- Chi Router
- GORM (ORM for Go)
- PostgreSQL (or any GORM-compatible database)
- Middleware for logging, recovery, and compression

## Project Structure
```
- internal/
  - config/         # Configuration handling
  - db/            # Database initialization
  - handler/       # HTTP handlers for API endpoints
  - middleware/    # Custom middleware
  - repository/    # Database repository layer
  - service/       # Business logic layer
```

## Installation

### Prerequisites
- Go 1.17 or later
- PostgreSQL (or any compatible database)

### Steps
1. Clone the repository:
   ```sh
   git clone https://github.com/golangTroshin/gophermat.git
   cd gophermat
   ```
2. Install dependencies:
   ```sh
   go mod tidy
   ```
3. Run the application:
   ```sh
   go run main.go
   ```

## Configuration
The application uses both environment variables and command-line flags for configuration. The settings are loaded using the `env` package and can be overridden with flags.

### Available Configuration Options:
| Environment Variable          | Flag | Default Value | Description |
|--------------------------------|------|--------------|-------------|
| `RUN_ADDRESS`                 | `-a` | `:8081`      | Server address and port |
| `DATABASE_URI`                | `-b` | `host=localhost user=gopheruser password=password dbname=gophermat port=5432 sslmode=disable` | Database connection string |
| `ACCRUAL_SYSTEM_ADDRESS`       | `-f` | `http://localhost:8080` | Accrual system address |
| `ACCRUAL_SYSTEM_WORKERS`       | `-w` | `2`          | Number of workers for the accrual system |
| `ACCRUAL_SYSTEM_INTERVAL`      | `-i` | `5`          | Interval for accrual system requests |
| `ACCRUAL_SYSTEM_RATE_LIMIT`    | `-r` | `5`          | Rate limit for accrual system |

These configurations can be provided through environment variables or modified using command-line flags at runtime.

## API Endpoints
### Authentication
- `POST /api/user/register` - Register a new user
- `POST /api/user/login` - Login an existing user

### User Operations (Requires Authentication)
- `POST /api/user/orders` - Upload an order
- `GET /api/user/orders` - Retrieve orders
- `GET /api/user/balance` - Get user balance
- `POST /api/user/balance/withdraw` - Withdraw balance
- `GET /api/user/withdrawals` - Get withdrawal history

## Graceful Shutdown
The application handles OS signals (`SIGTERM`, `SIGINT`) to allow a graceful shutdown, ensuring all ongoing processes are completed before termination.
