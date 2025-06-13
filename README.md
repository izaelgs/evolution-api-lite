# Evolution API Lite

This is a Docker-based setup for Evolution API Lite, which includes Redis and PostgreSQL services.

## Prerequisites

- Docker
- Docker Compose
- Git

## Getting Started

1. Clone the repository:
```bash
git clone git@github.com:izaelgs/evolution-api-lite.git
cd evolution-api-lite
cp .env.example .env
```

2. Create a `.env` file in the root directory with the following required variables:
```env
# Redis Configuration
CACHE_REDIS_ENABLED=true
CACHE_REDIS_URI=redis://localhost:6379
CACHE_REDIS_TTL=604800
CACHE_REDIS_PREFIX_KEY=evolution
CACHE_REDIS_SAVE_INSTANCES=false

# Database Configuration
DATABASE_PROVIDER=postgresql
DATABASE_CONNECTION_URI='postgresql://user:pass@localhost:5432/evolution?schema=public'

# Latest Whatsapp Web release (open web.whatsapp -> click on settings -> click on help section)
CONFIG_SESSION_PHONE_VERSION=2.3000.1023826371
```

3. Start the services:
```bash
docker-compose up -d
```

This will start:
- Evolution API on port 8080
- Redis on port 6379
- PostgreSQL on port 5432

## Service Information

### Evolution API
- Port: 8080
- Container Name: evolution_api
- Access: http://localhost:8080

### Redis
- Port: 6379
- Container Name: redis
- Persistence: Enabled (appendonly yes)
- Data Volume: evolution_redis

### PostgreSQL
- Port: 5432
- Container Name: postgres
- Database: evolution
- Username: user
- Password: pass

## Useful Commands

- View logs:
```bash
docker-compose logs -f
```

- View specific service logs:
```bash
docker-compose logs -f api    # For API logs
docker-compose logs -f redis  # For Redis logs
docker-compose logs -f postgres # For PostgreSQL logs
```

- Stop all services:
```bash
docker-compose down
```

- Restart all services:
```bash
docker-compose restart
```

## Troubleshooting

1. If Redis connection issues occur:
   - Check if Redis container is running: `docker ps`
   - Verify Redis logs: `docker-compose logs redis`
   - Ensure CACHE_REDIS_URI is correctly set in .env

2. If Database connection issues occur:
   - Check if PostgreSQL container is running: `docker ps`
   - Verify PostgreSQL logs: `docker-compose logs postgres`
   - Ensure DATABASE_URL is correctly set in .env

3. If API issues occur:
   - Check API logs: `docker-compose logs api`
   - Verify all environment variables are set correctly
   - Ensure all services are running: `docker-compose ps`

## Development

For development purposes, you can use the development configuration:
```bash
docker-compose -f docker-compose.dev.yaml up -d
```

## Volumes

The following volumes are created:
- evolution_instances: For API instance data
- evolution_redis: For Redis data persistence
- postgres_data: For PostgreSQL data persistence

## Networks

A bridge network named `evolution-net` is created for inter-service communication.

<h1 align="center">Evolution API Lite</h1>

<div align="center">

[![Whatsapp Group](https://img.shields.io/badge/Group-WhatsApp-%2322BC18)](https://evolution-api.com/whatsapp)
[![Discord Community](https://img.shields.io/badge/Discord-Community-blue)](https://evolution-api.com/discord)
[![Postman Collection](https://img.shields.io/badge/Postman-Collection-orange)](https://evolution-api.com/postman) 
[![Documentation](https://img.shields.io/badge/Documentation-Official-green)](https://doc.evolution-api.com)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue)](./LICENSE)
[![Sponsors](https://img.shields.io/badge/Github-sponsor-orange)](https://github.com/sponsors/EvolutionAPI)

</div>
  
<div align="center"><img src="./public/images/cover.png"></div>

## Introduction

**Evolution API Lite** is a lightweight version of the Evolution API, focusing solely on connectivity without the integrations and audio conversion features. It is designed to be more efficient and ideal for microservice environments where performance and simplicity are key.

## Core Features

- **WhatsApp Connectivity**: Provides connectivity via WhatsApp Web using the [Baileys library](https://github.com/WhiskeySockets/Baileys).
- **Official WhatsApp Cloud API**: Connects via Meta's official API for more reliable and scalable usage.

This version does not include integrations with external platforms like Typebot, Chatwoot, OpenAI or S3/Minio, and there are no audio conversion features. It's optimized for those who need fast, simple connectivity solutions.

## Telemetry Notice

To continuously improve our services, we have implemented telemetry that collects data on the routes used, the most accessed routes, and the version of the API in use. We would like to assure you that no sensitive or personal data is collected during this process. The telemetry helps us identify improvements and provide a better experience for users.

# Donate to the project.

#### Github Sponsors

https://github.com/sponsors/EvolutionAPI

## License

Evolution API Lite is licensed under the Apache License 2.0. See LICENSE for details.

© 2024 Evolution API