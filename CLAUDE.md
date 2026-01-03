infra-service-analytics, docker-compose, deployment, analytics, metrics

## Overview
- Docker Compose deployment for ADI Analytics API
- Query metrics, dashboards, and aggregated statistics
- Read-only service (no event ingestion)
- License: BSL-1.0

## Structure
- `docker-compose.yml` - Deployment configuration
- Builds from `../../crates/adi-analytics-api`

## Environment Variables
- `PORT` - Listen port (default: 8093)
- `DATABASE_URL` - PostgreSQL/TimescaleDB connection string (read-only queries)
- `RUST_LOG` - Log level (info, debug, trace)

## API Endpoints
All endpoints support `start_date` and `end_date` query parameters (ISO 8601).

### Overview
- `GET /api/analytics/overview` - Dashboard summary

### Users
- `GET /api/analytics/users/daily` - Daily active users
- `GET /api/analytics/users/weekly` - Weekly active users

### Tasks
- `GET /api/analytics/tasks/daily` - Task stats by day
- `GET /api/analytics/tasks/overview` - Task summary

### API Performance
- `GET /api/analytics/api/latency` - Endpoint latency stats
- `GET /api/analytics/api/slowest` - Slowest endpoints

### Health
- `GET /health` - Service health check

## Deployment
```bash
docker compose up -d
```

## URL
Production: https://adi.the-ihor.com/api/analytics

## Notes
- Read-only service (pairs with infra-service-analytics-ingestion)
- Queries TimescaleDB continuous aggregates for fast responses
- No write permissions needed on database
- Safe to scale horizontally
