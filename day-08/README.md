# Day 8 – Docker Troubleshooting and Health Checks

## Objective
Learn how to troubleshoot exited containers, investigate application errors, and monitor container health using Docker HEALTHCHECK.

## Tools Used
- Ubuntu Linux
- Docker Engine 29.1.3
- Docker Compose 2.40.3
- Nginx Alpine
- Python 3.12-slim

## Task 1 – Troubleshooting Exited Containers

Created a container with an intentional failure:

```bash
docker run --name broken-app ubuntu:latest sh -c "exit 1"
```

Checked container status:

```bash
docker ps -a
docker inspect broken-app --format='Status={{.State.Status}} ExitCode={{.State.ExitCode}}'
```

Result:

```text
Status=exited ExitCode=1
```

Key learning:
- Exit code 1 indicates a general application failure.
- Exit code 127 generally indicates command not found.
- `docker ps -a` displays stopped containers.

## Task 2 – Application Log Troubleshooting

Created a Python container with a missing application file:

```bash
docker run -d --name app-crash python:3.12-slim python missing.py
```

Inspected application logs:

```bash
docker logs app-crash
```

Observed error:

```text
python: can't open file '//missing.py':
[Errno 2] No such file or directory
```

Checked exit code:

```bash
docker inspect app-crash --format='Status={{.State.Status}} ExitCode={{.State.ExitCode}}'
```

Result:

```text
Status=exited ExitCode=2
```

Key learning:
- Application logs help identify the root cause.
- Missing Python dependencies can cause `ModuleNotFoundError`.
- Python dependencies should be installed during Docker image build using `requirements.txt` and a Dockerfile.

## Task 3 – Docker HEALTHCHECK

Created an Nginx Dockerfile:

```dockerfile
FROM nginx:alpine

HEALTHCHECK --interval=10s --timeout=3s --start-period=5s --retries=3 CMD wget -q --spider http://localhost/ || exit 1
```

Built the image:

```bash
docker build -t nginx-health:v1 .
```

Ran the container:

```bash
docker run -d --name nginx-healthy -p 8085:80 nginx-health:v1
```

Verified health:

```bash
docker ps
docker inspect nginx-healthy --format='Status={{.State.Status}} Health={{.State.Health.Status}}'
```

Result:

```text
Status=running Health=healthy
```

## Task 4 – Simulating an Unhealthy Container

Created a deliberately failing health check:

```dockerfile
FROM nginx:alpine

HEALTHCHECK --interval=5s --timeout=3s --retries=2 CMD wget -q --spider http://localhost/nonexistent || exit 1
```

Built and ran the test image.

Observed:

```text
Status=running Health=unhealthy
```

Inspected health-check logs:

```bash
docker inspect nginx-unhealthy --format='{{json .State.Health.Log}}'
```

Root cause:

```text
HTTP/1.1 404 Not Found
```

The requested `/nonexistent` endpoint returned HTTP 404, causing the health check to fail.

## Task 5 – Fixing the Health Check

Corrected the endpoint:

```dockerfile
FROM nginx:alpine

HEALTHCHECK --interval=5s --timeout=3s --retries=2 CMD wget -q --spider http://localhost/ || exit 1
```

Built and ran the corrected image:

```bash
docker build -f Dockerfile.unhealthy -t nginx-unhealthy:v2 .
docker run -d --name nginx-fixed -p 8086:80 nginx-unhealthy:v2
```

Verified:

```bash
docker inspect nginx-fixed --format='Status={{.State.Status}} Health={{.State.Health.Status}}'
curl -I http://localhost:8086
```

Final result:

```text
Status=running Health=healthy
HTTP/1.1 200 OK
```

## Important Docker Troubleshooting Commands

```bash
docker ps -a
docker logs container-name
docker inspect container-name
docker inspect container-name --format='{{.State.ExitCode}}'
docker stats
docker inspect container-name --format='{{json .State.Health.Log}}'
```

## Key Learnings

- Diagnosed exited Docker containers.
- Understood common exit codes.
- Used application logs to identify failures.
- Understood missing Python dependencies.
- Configured Docker HEALTHCHECK.
- Simulated and fixed unhealthy containers.
- Verified application health using Docker inspect and curl.

## Important Interview Concepts

- Running does not necessarily mean healthy.
- An unhealthy container may still have its main process running.
- Docker HEALTHCHECK reports health status but does not automatically restart an unhealthy container.
- Dependencies should be installed during image build for reproducibility.

## Result

Successfully completed practical Docker troubleshooting exercises and configured working health checks for Nginx containers.

**Status: Day 8 Completed**
