# Day 7 – Docker Compose: Multi-Container Application

## Objective
Learn how to build and manage a multi-container application using Docker Compose.

## Tools Used
- Ubuntu Linux
- Docker Engine 29.1.3
- Docker Compose 2.40.3
- Nginx Alpine
- Python 3.12

## Project Architecture

The application contains two services:

1. **Web (Nginx):** Serves the frontend HTML page on port 8084.
2. **Backend (Python):** Runs a Python HTTP server on port 5000.

Nginx forwards requests from `/api/` to the backend using Docker Compose service discovery.

## Project Structure

```text
docker-compose-practice/
├── backend/
│   ├── Dockerfile
│   └── server.py
├── web/
│   ├── index.html
│   └── default.conf
└── compose.yaml
```

## Docker Compose Concepts

- `services`: Defines application containers.
- `build`: Builds an image from a Dockerfile.
- `ports`: Publishes container ports to the host.
- `expose`: Documents ports intended for inter-container communication.
- `volumes`: Mounts host files into containers.
- `depends_on`: Controls service startup order.
- Default network: Allows containers to communicate using service names.

**Important:** Short-form `depends_on` controls startup order but does not guarantee application readiness.

## Important Commands

```bash
docker compose version
docker compose config
docker compose up -d --build
docker compose ps
docker compose logs --tail=50
docker compose logs backend
docker compose exec web nginx -t
docker compose down
```

## Application Testing

### Test frontend

```bash
curl http://localhost:8084
```

Expected result: HTML page displaying "Hello from Docker Compose!"

### Test backend through Nginx

```bash
curl http://localhost:8084/api/
```

Expected result:

```text
Hello from Docker Compose Backend!
```

## Nginx Reverse Proxy

The Nginx configuration forwards API requests to:

```nginx
location /api/ {
    proxy_pass http://backend:5000/;
}
```

Docker Compose provides internal DNS resolution for the `backend` service name.

## Troubleshooting Commands

```bash
docker compose ps
docker compose logs --tail=50
docker compose port web 80
docker compose exec web nginx -t
docker compose exec web wget -O- http://backend:5000/
```

## Key Learnings

- Created and managed multiple containers using one Compose file.
- Connected frontend and backend using a Docker network.
- Learned service-name-based DNS resolution.
- Configured Nginx as a reverse proxy.
- Tested frontend and backend communication.
- Practised Docker Compose troubleshooting.

## Result

Successfully deployed a two-service application using Docker Compose. The Nginx frontend and Python backend ran successfully, and the backend response was accessible through the Nginx reverse proxy.

**Status: Day 7 Completed**
