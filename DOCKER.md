# Docker Deployment Guide

This guide will help you containerize and run the Reporting Application using Docker.

## Prerequisites

- Docker 20.x or higher installed
- Docker Compose 2.x or higher installed
- Supabase project credentials

## Quick Start

### 1. Clone and Setup

```bash
# Navigate to the project directory
cd reporting

# Copy the example environment file
cp .env.example .env
```

### 2. Configure Environment Variables

Edit the `.env` file with your Supabase credentials:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_anon_key_here
NODE_ENV=production
```

### 3. Build and Run

```bash
# Build and start the container
docker-compose up -d

# View logs
docker-compose logs -f
```

The application will be available at `http://localhost:3000`

## Docker Architecture

### App Service

**Next.js Application**
- Multi-stage Docker build process:
  - Dependencies Stage: Installs production dependencies
  - Builder Stage: Compiles the Next.js application
  - Runner Stage: Serves the optimized standalone build
- Runs on port 3000
- Features:
  - ✅ Multi-stage build for smaller image size
  - ✅ Security: Runs as non-root user
  - ✅ Production optimizations enabled
  - ✅ Standalone output for minimal dependencies
  - ✅ Alpine-based image for reduced size

## Common Commands

### Managing Containers

```bash
# Start container
docker-compose up -d

# Stop container
docker-compose down

# Restart container
docker-compose restart

# View logs
docker-compose logs -f app
docker-compose logs -f        # All logs

# Execute commands in container
docker-compose exec app sh
```

### Rebuilding

```bash
# Rebuild after code changes
docker-compose up -d --build

# Rebuild without cache
docker-compose build --no-cache
```

### Troubleshooting

```bash
# Check container status
docker-compose ps

# View resource usage
docker stats

# Inspect container
docker inspect reporting-app

# Remove all containers and volumes
docker-compose down -v
```

## Manual Docker Commands

If you prefer not to use Docker Compose:

### Build

```bash
docker build -t reporting-app .
```

### Run

```bash
docker run -d \
  --name reporting-app \
  -p 3000:3000 \
  -e NEXT_PUBLIC_SUPABASE_URL=your_url \
  -e NEXT_PUBLIC_SUPABASE_ANON_KEY=your_key \
  reporting-app
```

### Stop and Remove

```bash
docker stop reporting-app
docker rm reporting-app
```

## Image Size Optimization

The current Dockerfile uses:
- Alpine Linux base image for minimal size
- Multi-stage builds to exclude build dependencies
- Next.js standalone output mode
- Production-only dependency installation

Expected image size: ~200-300 MB

## Network Configuration

The Docker Compose setup creates a custom bridge network (`reporting-network`) for better isolation and future scalability.

## Health Checks

To add health checks, update `docker-compose.yml`:

```yaml
healthcheck:
  test: ["CMD", "wget", "--no-verbose", "--tries=1", "--spider", "http://localhost:3000"]
  interval: 30s
  timeout: 10s
  retries: 3
  start_period: 40s
```

## Production Considerations

1. **Environment Variables**: Never commit `.env` files with real credentials
2. **Secrets Management**: Consider using Docker secrets or external secret management
3. **Resource Limits**: Add resource constraints in production
4. **SSL/TLS**: Configure SSL certificates for HTTPS using a reverse proxy or cloud provider
5. **Monitoring**: Add logging and monitoring solutions
6. **Backup**: Ensure database backups are configured
7. **Reverse Proxy**: Consider using Nginx or Traefik in front of the container for production

## Troubleshooting

### Build Fails

```bash
# Clear Docker cache and rebuild
docker-compose build --no-cache --pull
```

### Container Won't Start

```bash
# Check logs for errors
docker-compose logs app

# Verify environment variables
docker-compose config
```

### Port Already in Use

```bash
# Change port in docker-compose.yml
ports:
  - "8080:3000"  # Access on localhost:8080
```

### Memory Issues

Increase Docker Desktop memory allocation or add resource limits:

```yaml
deploy:
  resources:
    limits:
      memory: 1G
```

## Support

For issues or questions, please refer to:
- [Docker Documentation](https://docs.docker.com/)
- [Next.js Docker Documentation](https://nextjs.org/docs/deployment#docker-image)
- Project README.md
