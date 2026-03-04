# ERP OMEGA - Deployment Guide

This document provides instructions for hosting the ERP OMEGA system in a production or staging environment.

## 1. Prerequisites
- Docker & Docker Compose
- Node.js 20+ (for local builds)
- SQLite (built-in) or a production PostgreSQL instance.

## 2. Docker Deployment (Recommended)
The easiest way to host ERP OMEGA is using Docker Compose.

1.  **Configure Environment**:
    Create a `.env` file in the root directory (use `.env.example` as a template).
2.  **Start Services**:
    ```bash
    docker-compose up -d --build
    ```
3.  **Access the App**:
    - **Frontend**: `http://localhost` (Port 80)
    - **Backend**: `http://localhost:3000`

## 3. Security Considerations
- **Environment Variables**: Ensure `JWT_SECRET` is set to a long, random string.
- **SSL/TLS**: Use a reverse proxy like **Nginx** or **Traefik** in front of the Docker containers to handle HTTPS.
- **Rate Limiting**: Currently configured in `main.ts` to 100 requests per 15 mins per IP. Adjust based on load.
- **CORS**: Update `ALLOWED_ORIGINS` in your environment to match your production domain.

## 4. Maintenance
- **Database Backup**: Regularly backup `apps/api/prisma/dev.db`.
- **Logs**: View service logs using `docker logs -f erp-omega-api-1`.
