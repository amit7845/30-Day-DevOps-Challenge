# Day 9 – Docker Networking Troubleshooting

## Objective
Practice troubleshooting Docker networking issues, including DNS resolution, connection refused errors, service binding, and port publishing.

## 1. Custom Bridge Network
Created a custom Docker bridge network named `devops-day9`.

Command: `docker network create --driver bridge --subnet 172.18.0.0/16 devops-day9`

## 2. Container-to-Container DNS
Created backend and frontend containers on the same network.

Commands:
- `getent hosts backend`
- `curl http://backend:5000`

Result: Backend hostname resolved successfully, and HTTP connectivity worked.

## 3. DNS Failure
Disconnected the frontend from the network using `docker network disconnect devops-day9 frontend`.

Result: Backend hostname could not be resolved.

Fix: Reconnected using `docker network connect devops-day9 frontend`. DNS and connectivity worked again.

## 4. Connection Refused
Started a Python HTTP server bound to `127.0.0.1`.

Result: DNS worked, but the frontend could not connect to the service.

Root cause: The service was listening only on the container's loopback interface.

Fix: Recreated the backend using `--bind 0.0.0.0`.

Result: Container-to-container HTTP connectivity worked.

## 5. Port Publishing
Initially, the container had no published host port.

Result: `curl http://localhost:5000` failed on the EC2 host.

Fix: Recreated the container with `-p 5000:5000`.

Verified using:
- `docker port backend-test`
- `curl http://localhost:5000`

Result: Host access worked successfully.

## 6. Key Learnings
- User-defined bridge networks allow container communication.
- Docker DNS resolves container names on the same user-defined network.
- `getent hosts` checks hostname resolution.
- `127.0.0.1` listens only on loopback.
- `0.0.0.0` listens on all container interfaces.
- `-p HOST_PORT:CONTAINER_PORT` publishes a container port.
- `docker network connect` attaches an existing container to a network.
- `docker port` displays published port mappings.

## 7. Troubleshooting Commands
- `docker ps -a`
- `docker network ls`
- `docker network inspect devops-day9`
- `docker inspect backend-test`
- `docker logs backend-test`
- `docker port backend-test`
- `getent hosts backend-test`
- `curl http://localhost:5000`

## 8. Interview Assessment
Score: 5/5

Topics covered:
- Docker bridge networking
- DNS resolution
- Connection refused
- Service binding
- Port publishing

## Conclusion
Completed hands-on Docker networking troubleshooting by reproducing and fixing DNS, connectivity, and port publishing problems.
