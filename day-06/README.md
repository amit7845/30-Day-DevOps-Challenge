# Day 6 - Docker Networking

## Objectives
- Understand Docker bridge networking
- Create custom Docker networks
- Connect containers to networks
- Test container-to-container communication
- Understand Docker DNS
- Troubleshoot network isolation
- Configure port mapping

## Practical Tasks Completed

1. Verified Docker default networks.
2. Created custom bridge network devops-task.
3. Created app-server and app-client containers.
4. Tested communication using container names.
5. Verified container DNS resolution.
6. Inspected network configuration and container IPs.
7. Created isolated-network.
8. Reproduced a network isolation issue.
9. Connected an existing container to devops-task.
10. Verified connectivity with ping.
11. Deployed Nginx with host port 8083 mapped to container port 80.
12. Verified HTTP 200 OK.
13. Cleaned up temporary containers and networks.

## Important Commands

- docker network ls
- docker network create devops-task
- docker network inspect devops-task
- docker network connect devops-task isolated-client
- docker network rm devops-task
- docker run -dit --name app-server --network devops-task ubuntu:latest bash
- docker exec app-client ping -c 4 app-server
- docker run -d --name nginx-network -p 8083:80 nginx:latest
- docker port nginx-network
- curl -I http://localhost:8083

## Result

Successfully demonstrated container-to-container communication,
Docker DNS, network isolation, network troubleshooting and port mapping.

## Key Learning

Custom Docker bridge networks allow containers to communicate
using container names through Docker DNS.

Port mapping exposes container services through host ports.
